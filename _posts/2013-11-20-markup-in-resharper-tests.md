---
title: Markup in ReSharper Tests
author: sven
layout: article
permalink: /blog/2013/11/markup-in-resharper-tests/
categories:
  - ReSharper
tags:
  - testing
---
<a href="http://confluence.jetbrains.com/display/NETCOM/2.10+Testing+%28R8%29#2.10Testing%28R8%29-TestDataMarkup" title="ReSharper 8 - Test-Data Markup" target="_blank">Test Data Markup</a> is a way to provide meta information about test cases in R# tests. A simple case is the caret position, designated by `{caret}`. This markup element is placed in the source code, directly where the caret is intended to be. Other markup allows to define test settings. Such settings can be queried by `GetSetting()` in test class, for example, to switch certain test behavior. An important piece of information missing in the R# documentation is that such settings need to be placed in comments:

<pre class="brush: csharp; title: TestDataFile.cs; notranslate" title="TestDataFile.cs">// ${SETTING_NAME:VALUE}

class Demo { ... }
</pre>