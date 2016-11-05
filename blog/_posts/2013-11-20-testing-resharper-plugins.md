---
title: Test ReSharper Plugins
author: sven
layout: article
tags:
  - Visual Studio
  - ReSharper
  - Functional Testing
  - Testing
comments: true

---

First thing you have to understand, when it comes to <a title="ReSharper 8 - Testing" href="http://confluence.jetbrains.com/display/NETCOM/2.10+Testing+%28R8%29" target="_blank">R# test projects</a>, is that they are really meant for <a title="Functional Testing - Wikipedia" href="http://en.wikipedia.org/wiki/Functional_testing" target="_blank">functional testing</a>. When you run the tests, R# starts an in-memory R# environment (that is what takes so long), loads your test data, and only then actually executes your tests.

<!--more-->

<p style="padding-left: 30px;">
  <strong>Attention:</strong> A R# environment is not a VisualStudio environment. This means that in your integration tests you cannot access anything specific to VisualStudio. Especially, <a title="ReSharper 8 - Exposed VisualStudio Interfaces" href="confluence.jetbrains.com/display/NETCOM/2.02+Component+Model+(R8)#2.02ComponentModel(R8)-Defaultlistofexposedinterfaces" target="_blank">the exposed VisualStudio interfaces</a> are not available. See <a title="How To: Use VisualStudio Dependencies in R# Plugins" href="http://sven-amann.de/blog/2013/11/how-to-use-visualstudio-dependencies-in-r-plugins/">my post about VisualStudio dependencies in R# plugins</a> for an approach that solves this.
</p>

While the R# documentation explains you how to set up a <a title="Setup a ReSharper Test-Environment Assembly" href="http://confluence.jetbrains.com/display/NETCOM/2.10+Testing+%28R8%29#2.10Testing%28R8%29-TestEnvironmentAssembly" target="_blank">Test-Environment Assembly</a>, it&#8217;s rather implicit about how to actually write a test. I figured it out, by looking at existing tests, i.e., subclasses of `BaseTest` (thanks to Matt Ellis <a title="ReSharper-API-Forum" href="http://devnet.jetbrains.com/message/5502880#5502880" target="_blank">for this pointer</a>!). Classes that contain `TestBase` or `BaseTest` in their names are meant to be subclassed by actual tests.

Unfortunately, the base-tests do not include much documentation and I was not able to find the data files of that the concrete tests distributed with R#. I found some helpful examples, in the public repository of the R# extension [PostfixCompletion][1].

All the test I had a look at so far follow the same scheme:

  1. They load some test data into a virtual solution/project,
  2. then they execute some action(s) and record the result in a text file,
  3. and, finally, they compare the result file against a so called gold file.

I&#8217;ll go through these steps, one by one.

## Test Intention

For the sake of this example, I assume that I have implemented an extension for the code completion that provides an additional LookupItem named &#8220;Foo&#8221; whenever completion is triggered on an arbitrary instance reference. I want to test that this proposal actually appears in the list of items provided by the code completion.

I pick the CodeCompletionTestBase as the base-test. The name sounds right. The test skeleton looks like this:

{% highlight csharp %}
using JetBrains.ReSharper.Feature.Services.Test.CSharp.FeatureServices.CodeCompletion;
using JetBrains.ReSharper.TestFramework;
using NUnit.Framework;

[TestFixture, TestNetFramework4]
public class CodeCompletionListTest : CodeCompletionTestBase
{
    [Test]
    public void TestFooLookupItem()
    {
        ...
    }

    protected override bool ExecuteAction
    {
        get { return false; }
    }
}
{% endhighlight %}

The property `ExecuteAction` is declared abstract in the base class. Executing the action means that the code completion will be committed and the result of the transformation will be tested. Not executing the action will result in the item list to be checked. This is what I want, hence, I set the property to `false`.

## Test Data

As I already explained, the test is going to run on some test data, i.e., some code in which a code completion is invoked. Such test data is to be placed below

{% highlight text %}
%TestProjectDir%/testdata
{% endhighlight %}

The sub-path of a concrete test&#8217;s test data is determined by the test class&#8217;s `RelativeTestDataPath` property, which I override for my test like so:

{% highlight csharp %}
protected override string RelativeTestDataPath
{
    get { return "CodeCompletion\\FooLookupItem"; }
}
{% endhighlight %}

I define a first test scenario in the following file

<figure>
{% highlight csharp %}
class HappyPath
{
    void Method(object obj)
    {
        obj.{caret}
    }
}
{% endhighlight %}
  <figcaption>File: %TestData%/CodeCompletion/FooLookupItem/HappyPath.cs</figcaption>
</figure>

It&#8217;s a minimal code snippet necessary to trigger code completion on some instance reference. The [marker][2] {caret} tells R# were to place the caret before executing the test.

**Attention:** In VisualStudio you cannot add this file to your project, since the markup renders it uncompilable, what prevents test execution. This means that you have to manage the files outside VisualStudio and that VisualStudio will not keep track of the test-data files&#8217;s version-control status&#8230; An alternative is to <a title="ReSharper 8 - Test-Data File Extensions" href="http://confluence.jetbrains.com/display/NETCOM/2.10+Testing+%28R8%29#2.10Testing%28R8%29-ANoteonFileExtensions" target="_blank">change the default file extension for test-data files</a>.

## Test Execution

To make the test run with the newly created data file, I insert the call

{% highlight csharp %}
DoOneTest("HappyPath")
{% endhighlight %}

into the test method in the skeleton. On execution, R# loads the file into a virtual test project, opens the file, and places the caret at the marked position. The base-test then triggers the code completion at the current caret position and captures the LookupItem list.

When I run the test at this point (by executing Unit Test in the test project), the test fails with an error message saying that the gold file for the test was not found. The output generated by the test, i.e., the line-wise serialization of the encountered LookupItem list, can afterwards be found in the file

{% highlight text %}
%TestData%/CodeCompletion/FooLookupItem/HappyPath.cs.tmp
{% endhighlight %}

## Gold File

To complete my test case, I add the expected test outcome, i.e., the gold file. For the happy-path test it looks like this:

<figure>
{% highlight text %}
+ Equals
Foo
+ GetHashCode
+ GetType
+ MemberwiseClone
+ Method
+ ToString
{% endhighlight %}
  <figcaption>%TestData%/CodeCompletion/FooLookupItem/HappyPath.cs.gold</figcaption>
</figure>

**Note:** The + designates preferred items, what follows after is the display name as shown in the IDE. The list is ordered alphabetically by the base-test.

Now the test passes, as the contents of the tmp file and the gold file match. As a result, the tmp file is deleted after the test run.

## Conclusion

Carrying all the bits and pieces together, I managed to write a first test for my R# extension. I can now easily add a second test case, by creating another code and corresponding gold file and adding a second test method or making the existing method a `TestCase`, parameteric in the test file&#8217;s name.

The hard part about this was to find the right base-test and to understand the data files it expects. Unfortunately, there is no documentation about this and the base-tests themselves are pretty hard to read. At least for me. Also, they are not as extendable as I would wish. For example, I cannot easily change the gold-file format, to include additional information from the LookupItems. In order to do that I would have to copy most of `CodeCompletionTestBase`.

What&#8217;s more: there are test switches coded into the base-tests. For example, if you set `ExecuteAction` to `true`, the test will check the outcome of committing the code completion. This requires you to add the [test setting][2] `COMPLETE_ITEM` to the test data file and to change the gold files to a modified version of the code snippets, as you expect it to look like after the `COMPLETE_ITEM` was chosen from the completion. There are several other switches in the base-test that you can use to test various aspect of the code completion. Sadly, you only way to find out about them is to look into the code&#8230;

 [1]: https://github.com/controlflow/PostfixCompletion
 [2]: http://sven-amann.de/blog/2013/11/markup-in-resharper-tests/ "Markup in ReSharper Tests"