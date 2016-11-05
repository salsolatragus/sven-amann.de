---
title: About Actions.xml
author: sven
layout: article
tags:
  - ReSharper
comments: true

---

`Actions.xml` is the nice little configuration how your R# actions are added to the menus. I recently found myself in a situation where my menu items didn&#8217;t show up, even though I copied over the configuration from a playground project where it worked.

Frist thing you want to check is that the `ActionsXml` attribute is set in your `AssemblyInfo.cs`:

{% highlight csharp %}
[assembly: ActionsXml("%assembly-name%.Actions.xml")]
{% endhighlight %}

Note that the file itself is actually called `Actions.xml` and placed in the project&#8217;s root. I&#8217;m not quite sure whether the prefix actually is the assembly or the project name, my guess is for assembly name, though.

Second thing you want to check is that the `Action.xml` is included as an &#8220;Embedded Resource&#8221;. To do so, go to the file&#8217;s properties and select &#8220;Embedded Resource&#8221; for the property &#8220;Build Action&#8221;. This is required if you copied the file in, because Visual Studio will set the property to &#8220;Content&#8221; then. Took me a couple of hours to figure out this one&#8230;

Fixing these two thing did the job for me.