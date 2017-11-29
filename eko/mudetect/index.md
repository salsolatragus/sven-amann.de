---
title: MuDetect - Find and Fix API Misuses
author: Sven
layout: article
image:
  thumb: mudetect_logo.png

---

<img style="float:right;" src="../../images/mudetect_logo.png" alt="MuDetect Logo" width="300" height="333" />
Again and again software crashes, because developers use APIs incorrectly. A classic example is when someone uses the API of a Java collection in a way that leads to a ConcurrentModificationException. We call such mistakes *API Misuses*. Often, missing or incomplete documentation, unwillingness to read documentation, bad API design, careless mistakes, update of APIs, or a combination of these cause API misuse. [The MuBench study](/publications/2016-05-MSR-MUBench-dataset/) shows that API misuse cause problems both during development as well as after releases and that 7 of 10 misuses lead to software crashes.

I believe that it does not need to be this way. Therefore, I started [the Software Campus Project Eko](/eko/), a cooperation between [Technische Universität Darmstadt](http://www.stg.tu-darmstadt.de/) and [DHL IT Services](https://www.dpdhl.com/en/about_us/corporate_divisions/it_services.html). Together, we develop *MuDetect*, an assistance tools that warns developers of API misuses. The idea behind MuDetect is to employ machine-learning techniques to learn correct API-usage patterns from existing source code and to automatically detect violations of such patterns. So far, our experiments indicate that the idea works quite well.

The detection of API misuses is, of course, only the first step, because when the problem is identified, it still needs to be fixed! Therefore, we develop techniques to automatically derive fixes for a given violation from the usage patterns that they violate.