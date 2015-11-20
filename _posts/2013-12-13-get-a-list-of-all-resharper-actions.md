---
title: Get a List of All ReSharper Actions
author: sven
layout: article
permalink: /blog/2013/12/get-a-list-of-all-resharper-actions/
categories:
  - How To
  - ReSharper
tags:
  - 'c#'
---
Have you ever wondered what ReSharper actions there are or searched whether there is some ReSharper action triggered by a certain user interaction that you want to handle? It&#8217;s actually fairly easy to find out what&#8217;s there. Just add the following class to your ReSharper plugin, run it in debug mode, and check the console output.

<pre class="brush: csharp; title: ; notranslate" title="">using JetBrains.ActionManagement;
using System.Diagnostics;

[ShellComponent]
public class MyReSharperActionIdPrinter
{
    public MyReSharperActoinIdPrinter(IActionManager actionManager)
    {
        actionManager.GetAllActions().Cast&lt;IUpdatableAction&gt;().ForEach(action =&gt; Debug.WriteLine(action.Id));
    }
}
</pre>

**Note**: IExecutableAction is a subtype of IUpdatableAction, so this really works for all registered actions.