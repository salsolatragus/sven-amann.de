---
title: Test Jekyll Builds
author: sven
layout: article
tags:
  - Jekyll
  - Continuous Integration
  - Testing
comments: true

---

When I recently [set up a Travis build for my website](http://sven-amann.de/blog/2016/12/jekyll-post-from-ios/), I came across several sources mentioning automated testing of Jekyll pages. Of course that got me curious. After all, what's CI without test? <!--more--> Part of what I ended up adding to my site's build is from [an article by Jacob Tomlinson](https://www.jacobtomlinson.co.uk/jekyll/2015/02/18/test-you-jekyll-blog-with-travis-ci/). I'll repeat those parts that I found useful and add my additional insights while I go along. 

# What to Test?
The idea of testing a website may not appear as straightforward as the idea of testing software, but ultimately Jekyll generates a piece of machine-readable output (HTML) from the page sources and we might as well ensure some properties of that output via automated tests.

To me, the most obvious property is that all links, both external and internal, point to existing destinations. This property may be violated by me, e.g., when I add a broken link in the first place or when I move parts of my page. It might as well be violated by somebody else, e.g., if some other page becomes unavailable at some point. I'll most likely not check this by hand all too often, so why not have the build do it for me?

Other properties are standard compliance, e.g., with the HTML specification or accessibility standards. In a Jekyll context HTML compliance is mostly a property of the template in use, but special content of individual pages may certainly mess this up as well. Also, in my experience, automated checkers are the only sensible way to ensure compliance here anyways, so why not make those part of CI? Accessibility-standards require the presence of certain markup, such as `alt` attributes for images, which are easily forgotten and as easily script checked. Another good candidate for automated testing. 

# Setup Testing
Since my build was already running, I merely needed to add respective checks. A widely used tool for this purpose is [HTML Proofer](https://github.com/gjtorikian/html-proofer), which is available as a ruby gem and can, as such, easily be integrated into a Jekyll-page build. First, I added the respective dependency to my `Gemfile`:

{% highlight bash %}
gem 'html-proofer'
{% endhighlight %}

Next, I added an invocation of the tool to my build configuration:

{% highlight yaml %}
script:
  - ...
  - bundle exec htmlproofer ./_site --http-status-ignore "999" --url-swap "https?\:\/\/(127\.0\.0\.1\:4000|localhost\:4000|sven-amann\.de):" --check-html
 
env:
  global:
    - NOKOGIRI_USE_SYSTEM_LIBRARIES=true # speeds up installation of html-proofer
{% endhighlight %}

By default, HTML Proofer follows all links in the generated website and ensures that their destinations exist. It ensures that all referenced images exist and checks whether they have `alt` attributes. By adding the `--check-html` option, I told it to additionally check that the generated HTML is well formed, using [Nokogiri](http://www.nokogiri.org/tutorials/ensuring_well_formed_markup.html). This throws errors for mistakes, such as missing closing tags or duplicated attributes.

To make the link checks work for me, I had to do some additional configuration:

* Some pages, such as LinkedIn and Slideshare, apparently [refuse requests depending on the user agent or other properties](https://github.com/gjtorikian/html-proofer/issues?q=is%3Aissue+is%3Aclosed). This makes respective link checks fail. Fortunately, theses requests seem to consistently result in the status code 999, which allows to filter these cases by adding `--http-status-ignore "999"`.
* HTML Proofer cannot distinguish absolute URLs to the generated site from external URLs. Therefore, the contents of the currently published site will be checked, rather than the contents of the site-under-test. I use the `--url-swap` option to solve this problem, by replacing any match of the regular expression (before the colon) by the empty string (after the colon). This effectively converts any absolute URL to my site, such as "http://sven-amann.de/blog/foo", into its relative equivalent, e.g., "/blog/foo". I added "localhost" and "127.0.0.1" for this to also effect manual test runs in my local development environment. 

HTML Proofer provides the option `--only-4xx` to restrict link-check failures to only such that return a 4xx status code. This excludes, for example, internal server errors of external targets, which might be temporary and are mostly out of my control. For now, however, I decided against specifying this option, to get notified about any broken link. Let's see if I come to rue this decision.

# Conclusion
Running this for the first time, I immediately found two broken Links in my blog posts, one of which I could update, while I had to replace the second with a footnote saying that the respective page is no longer available. Hence, testing already fulfilled its purpose.

If you have other ideas for tests to add thoughts about this, please share them with me!
