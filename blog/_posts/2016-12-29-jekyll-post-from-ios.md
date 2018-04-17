---
title: Edit a Jekyll Website from iOS
author: sven
layout: article
tags:
  - Jekyll
  - Blogging
  - iOS
  - Travis
  - Continuous Integration
  - GitHub
comments: true

---

A while ago, I moved my website and blog to Jekyll. Good decision. No more Wordpress vulnerabilities, less bling bling, more control. Only drawback: I can no longer blog from my tablet. Well... I couldn't. Here comes my first Jekyll post from my iPad. 

My original Jekyll workflow was to edit and build the site on my laptop and, subsequently, publish it via FTP. The main problem that kept me from doing the same on my tablet was that I cannot run a Jekyll build there. Moreover, I needed a way to deploy updates from my tablet via FTP and to synchronize changes between my laptop and tablet.

First things first. Since I cannot build on my tablet, I need to build somewhere else. I already kept my site in a GitHub repository, but GitHub's out-of-the-box Jekyll support fails to build my site, because I use `pygments`. Therefore, I turned to a custom Jekyll build with [Travis](http://travis-ci.org). This has been done before and is even [in the official Jekyll documentation](https://jekyllrb.com/docs/continuous-integration/). I did some adaptations for my cause that led to this `.travis.yml`:

{% highlight yaml %}
language: ruby
rvm:
- 2.3.1
cache: bundler

install:
- bundle install
script:
- bundle exec jekyll build
{% endhighlight %}

This solves the build problem. Next, I needed a way to deploy the resulting site via FTP to my web space. Turned out this is surprisingly easy, using `ncftp` for the upload and [Travis's encryption feature](https://docs.travis-ci.com/user/environment-variables/) to hide my credentials. All I had to do was add two commands for execution after a successful build:

{% highlight yaml %}
addons:
  apt:
    packages:
      - ncftp

after_success:
- ncftpput -R -v -u "$FTP_USER" -p "$FTP_PASS" $FTP_HOST / ./_site/*
{% endhighlight %}

The first command installs `ncftp` in the CI environment, while the second uploads all contents of `./_site/` (recursively) to my FTP root. This solves the deployment problem.

Using GitHub gives me synchronization between edit devices for free. All I needed was to find a way to work on a git repository from my tablet. Turns out there's [Working Copy](https://appsto.re/de/xONC1.i) to do just that, including basic editing and syntax highlighting. The app also [integrates with a couple of more advanced code editors for iOS](https://workingcopyapp.com/#extending-ios), which I didnt try yet. This solves the editing problem.

It took me some time to figure this all out and to actually decide how I wanted this to work. Hope this post saves you some time. If you have any questions or problems, feel free to ask. Maybe I can help. 