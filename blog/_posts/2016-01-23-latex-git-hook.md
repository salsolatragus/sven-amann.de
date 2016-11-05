---
title: A LaTeX Git Hook
author: sven
layout: article
tags:
  - LaTeX
  - git
comments: true

---

I manage my LaTeX documents in git. I love it. It's good for the sanity of both me and my collaborators. Only sometimes, someone commits a broken document and whoever tries to compile it next has to figure out the error. Not always an easy task with LaTeX. What if there where an easy way to prevent this from happening?

<!-- more -->

In software engineering, we have IDEs that continuously build or code, so we immediately see when we break it. People use build servers to prevent broken stuff to end up in their repositories. What if we could do the same for LaTeX documents?

No worries, I'm not going to tell you to set up a build server for every LaTeX document you create. There's an easier solution. Use a git pre-commit hook to check if any of the LaTeX documents in you repository is outdated. And simply disallow commit, if one is.

Today, I've had it. And I build [such a LaTeX commit hook][1].

Feel free to use and distribute it. And please tell me what you think!

 [1]: https://github.com/salsolatragus/latex-git-hook