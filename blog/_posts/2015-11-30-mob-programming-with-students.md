---
title: Mob Programming with Students - Round 1
author: sven
layout: article
tags:
  - Mob Programming
comments: true

---

Today, I ran my first Mob Programming with students. After this experiment I am, even more than before, convinced that Mob Programming is an effective way to scale hands-on software development training to relatively large groups.

<!-- more -->

When I first learned about [Mob Programming][1] in a talk by [Woody Zuill][2] at [@OnAgile 2015][3], it struck me as a brilliant way to make hands-on training scale to at least the number of student assistants I employ. When I asked him, Woody confirmed that he had indeed already used the method in similar settings and kindly took the time to share his experience with me. 

Some months passed since, but today, I finally ran my first Mob Programming experiment with students. Five of my students volunteered for the events, one of which unfortunately got sick and could not participate. Two of the remaining students knew each other, while the others had not met before. Three of them are third year Bachelor students and one a first year Master student. Only one of them had heard of Mob Programming before my invitation.

I arranged the group according to the recommendations from the [Mob Programming Guidebook][4]: The students sat in a half-circle in front of a projector. The left-most student sat in front of the keyboard, playing the driver. He was not allowed to type unless instructed by the navigator. The right-most student was that navigator. He could discuss his ideas with the remaining two, who where also free to give suggestions at any time. In the feedback, the students stated that having one navigator as a decision maker helped them progress, although all non-drivers regularly contributed to discussions.

As an initial technical issue we identified that one student was used to a different keyboard layout, which was not natively supported by Windows. Luckily, we could quickly install the respective mapping scheme, such they could switch to their preferred layout when driving.

As a task, I asked the students to implement a basic Point of Sale (POS) for my small grocery store. First, I asked them to implement selling of individual items and later extended the task to selling multiple items. The output was to be printed to `stdout`. They worked for approximately 1:40 hours in total, followed by a feedback and discussion, which lasted for another 30 minutes. In retrospective, one of them noted that they should have taken a break after about an hour. All implementation was done in C# using Visual Studio. Two of the students had programmed C# in Visual Studio before, while the other two had no experience with neither.

We shifted seats ever 5 minutes, so that the navigator became the driver and one of the former observers became the navigator. After I gave them the initial task, I immediately started the timer for the first round. Even though I suggested for them to take some time for an initial planning, they immediately jumped into writing code. During the feedback they stated that the short cycle time put them under pressure and effectively kept them from thinking things through. Moreover, they critiqued that the cycling led to always the same pairs of driver and navigator.

It took the group about one full cycle (20 minutes) to warm to Mob Programming. Three of the five stated later that it was at first strange to work with people they had not met before. This kept them from openly critiquing the code they developed. This ice was finally broken during the 4th cycle, when they discovered that all of them had held back from commenting on a code issue that all of them had noticed.

Interestingly, already after the second full cycle they all handled the IDE and language with relative ease, including a growing number of shortcuts. Two of them stated that working under the guidance of the navigator and with the joint knowledge of the whole mob, it was much easer to get started with the unfamiliar tools.

Over the entire session, the group performed test-first programming. In the feedback, they noted this as a positive result of working in a mob, because they would not have done it on their own. All of them agreed that they jointly produced code with high quality. In fact, through their discussions, they repeatedly discovered additional test cases. Interestingly, they almost did not refactor or clean up neither their test nor their production code. When I asked them for this in the feedback, one student said that he had felt an increasing urge to do so, but that it had not yet been strong enough to act for it.

Looking back at these first two hours of Mob Programming with students, I am amazed by how fast the students adopted the style of working and how quickly they found themselves into language and IDE. Also it surprised me how quickly I, as an observer, got a pretty good picture of their individual skills. I am now, even more than before, convinced that Mob Programming helps to scale coding training to relatively large groups of students. I will take the mob's feedback to improve the setting next time. Also I want to enrich the task by methodological aspects, like finding good names, removing duplication, reducing the number of tests, or the like, to nudge the mob in directions it does not go on its own. I am very much looking forward to this.

 [1]: http://mobprogramming.org/mob-programming-basics/
 [2]: http://zuill.us/WoodyZuill/
 [3]: http://www.agilealliance.org/programs/onagile-virtual-conference/
 [4]: https://leanpub.com/mobprogrammingguidebook