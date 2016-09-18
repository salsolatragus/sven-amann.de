---
title: Software Campus Project Eko
author: Sven
layout: article
image:
  thumb: eko_logo.png
---
<img style="float:right;" src="../images/eko_logo.png" alt="Eko Logo" width="300" height="179" />
Reuse of existing software components is crucial in today's software-development projects. This requires software developers to be familiar with these components and with the best practices with respect to their usage. An enormous challenge, considering the number of frameworks, libraries, and technologies that emerged over the past years. Consequently, companies often invest considerably to train employees to become effective members of development teams.

In the [Software Campus][1] project [KaVE][2] my colleague Sebastian Proksch and I built developer-assistance tools that help writing new code, using existing software components. These tools, often referred to as *Recommender Systems for Software Engineering (RSSE)*, help developers to learn and use software components quickly and correctly. The foundation of our RSSEs are machine-learning techniques, which we use to automatically learn programming patterns from existing program code. Thereby, we bring the knowledge of entire developer communities directly into IDEs.

Today, the software industry not only faces the challenge of developing new software products, but also that of maintaining existing software solutions. Often, such legacy products depend on outdated third-party software components, because as these components change over time, updating the dependencies could introduce bugs due to changed usage patterns.

In my [Software Campus][1] project Eko, we develop [MuDetect][4], an assistance tool that supports developers in finding and fixing erroneous or non-best-practice usages of software components. Again, we employ machine-learning to discover usage patterns, to detect violations of them, and to suggest fixes for problems [MuDetect][4] discovers.

To evaluate the performance of [MuDetect][4] an similar approaches, we recently proposed [MuBench][5], a benchmark dataset and pipeline. Our experiments indicate that [MuDetect][4] outperforms other state-of-the-art detectors. A respective publication is currently under review.

In cooperation with my project partner [DHL IT Services][3], I want to deploy [MuDetect][4] in an industrial setting and evaluate how developers make use of it in their every-day work. Real-world studies like this are very costly, but present an enormous value to the research community. At the same time, the project improves the state-of-the-art tool chain of DHL's developers, helping them to build and maintain high-quality software even faster.

More information about the project are available on <a href="http://www.softwarecampus.de/aktuelles/forschungsprojekte/projekt/eko-intelligente-entwicklungswerkzeuge-zur-korrekten-wiederverwendung-bestehender-softwarekomponenten/" target="_blank">the official website of the Software Campus program</a> (German only).

 [1]: http://www.softwarecampus.de/
 [2]: http://kave.cc
 [3]: http://www.dpdhl.com/en/about_us/corporate_divisions/it_services.html
 [4]: /eko/mudetect/
 [5]: /publications/2016-05-MSR-MUBench-dataset.html
