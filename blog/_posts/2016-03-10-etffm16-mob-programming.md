---
title: Mob Programming @ETFFM16
author: sven
layout: article
tags:
  - MobProgramming
comments: true

---

Today, I ran an experiment. I formed a mob of conference participants and let them program an [MVP][1] of the [POS Kata][2] in (8 * 3 =) 24 min. This high-speed [mob programming][3] turned out to be a lot of fun and quite an experience for the volunteers, the audience, and myself.

<!-- more -->

In the past month, I facilitated several mob-programming sessions with students, each lasting 2-3 hours. I learned that a mob forms in about 1 hour. Unfortunately, at the "Frankfurter Entwicklertag 2016", I only got 45 minutes to introduce the concept, find volunteers, and let them practice. Considering that the conference is targeted at professional software developers, surely a random mob of them should achieve in about 30 minutes what students mobs manage in 60, right?

I took roughly 10 minutes to introduce the idea of mob programming and the setup of the experiment ([see my slides][4]). Then I asked for five volunteers. Four stepped forward quickly, a fifth --somebody with little coding experience-- joined hesitantly a little later.

With the mob assembled, I took a few more minutes to explain the task: Write a program that allows selling of individual times. Given a barcode, it shows the price associated with the respective product on a display. The barcode is represented as a string of digits terminated by a newline. It is passed to the program from somewhere, e.g., a barcode scanner, as an event. The output is send to a display that shows a single line of text at a time.

The mob rotated in 3-minute intervals, the navigator becoming the driver, the driver moving to the mob, and a new navigator emerging from the same. Initially, there was some confusion about what to do and where to go, but from second one the mob was having fun. After the first rotations, the process smoothed out considerably and they converged towards an agreeable solution. Unfortunately, we ran out of time already after 8 intervals (24 minutes). I'm happy with how the session went, but I would probably not do another with less than 90 minutes for programming.

In a quick retrospective, the members of the mob confirmed that it was a fun experience. They were not satisfied with their code, but happy that they managed to work in the same general direction. One noted that there was not too much discussion within the mob, but a several times someone other than the navigator (and once even someone from the audience) provided the right idea or piece of knowledge to advance. Three volunteers said later that they want to give mob programming a try in their real work environment, soon.

Overall, the experiment was a success. You should definitely run one yourself sometime!

 [1]: http://blog.jbrains.ca/permalink/what-makes-an-mvp
 [2]: http://online-training.jbrains.ca/courses/wbitdd-01/lectures/136762
 [3]: http://mobprogramming.org
 [4]: http://www.slideshare.net/SvenAmann/mob-programming-entwicklertag-frankfurt-2016
