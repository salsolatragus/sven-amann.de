---
title: 'Use VisualStudio Dependencies in R# Plugins'
author: sven
layout: article
tags:
  - Visual Studio
comments: true

---

Let&#8217;s assume you want to write a ReSharper plugin for use in VisualStudio. Respectively, this extension accesses services provided by VisualStudio, such as the <a href="http://msdn.microsoft.com/en-us/library/vstudio/envdte.dte.aspx" target="_blank"><code>DTE</code></a> (made available by <a href="http://confluence.jetbrains.com/display/NETCOM/2.02+Component+Model+%28R8%29" target="_blank">the ReSharper component model</a>) or even services only available via the `RawVsServiceProvider`. While this is generally fine, there are certain subtleties to consider when doing it.

<!--more-->

The main problem becomes apparent when you want to test your plugin with a R# integration-test project: The tests fail, because the VisualStudio dependencies cannot be injected. In <a href="http://devnet.jetbrains.com/thread/450709?tstart=0" target="_blank">a discussion with Matt Ellis</a> I found out that this is actually to be expected. R# is an environment generally intended for use independent of VisualStudio. Consequently, its test environment loads a standalone R# environment, where VisualStudio dependencies are not available. This has a drawback and an advantage:

  1. You cannot test your R# plugin&#8217;s integration into VisualStudio this way.
  2. You can replace you VisualStudio dependencies by custom mocks that allow you to control the environment in your tests.

The key to solve the issue is not to let your actual components depend directly on the VisualStudio dependencies, but to introduce a layer of abstraction in between, using R#&#8217;s component model. Let&#8217;s assume, for example, that you have a component named `MyComponent` that depends on a VisualStudio service called `SMessageBus`:

{% highlight csharp %}
[ShellComponent]
public class MyComponent
{
  public MyComponent(IMessageBus messageBus) { ... }
}
{% endhighlight %}

Now you make the dependency available in an VisualStudio environment by adding a component like the following to your plugin:

{% highlight csharp %}
[ShellComponent(ProgramConfigurations.VS_ADDIN)]
public class VsMessageBus : IMessageBus
{
  private readonly IMessageBus _messageBus;

  public VsMessageBus(RawVsServiceProvider serviceProvider)
  {
    _messageBus = serviceProvider.Value.GetService<SMessageBus, IMessageBus>();
  }

  // delegates from IMessageBus interface to _messageBus field
}
{% endhighlight %}

The `VS_ADDIN` argument passed to the `ShellComponent` attribute lets R# only instantiate this component in a VisualStudio environment. In this case, the `RawVServiceProvider` is available and the service can be retrieved. `VsMessageBus` is automatically registered to the R# component model as an implementation of `IMessageBus` and, thus, injected an creation of `MyComponent`.

In you test project, as it runs in a standalone R# environment, the `VsMessageBus` component is not loaded. To get your tests to run, you can add a mock implementation of `IMessageBus` to the test project, as a `ShellComponent`. As it is part of the test project, this mock will never be loaded in production mode. It can implement any behavior you need for you tests, e.g., capture all messages send to the bus in a list for later verification.

## A Word on Native VisualStudio Interfaces

After I figured out the above, I expected that for VisualStudio interface exposed by R#, such as `DTE`, one could save the effort of implementing the `VS_ADDIN` component. While this is true for running in a VisualStudio environment &#8212; the `DTE` instance is correctly injected &#8211;, injection of the mock component &#8212; implementing the `DTE` interface &#8212; in the test project still fails on me. To resolve this I had to introduce a custom interface

{% highlight csharp %}
public interface IVsDTE : DTE {}
{% endhighlight %}

and implement this interface with a component in both the production and the test code, as demonstrated for the `SMessageBus` service above.