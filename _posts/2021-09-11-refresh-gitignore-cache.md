---
title: I've updated .gitignore but the files are still tracked, what's the deal?
date: 2021-09-11 16:02:00 -0700
categories: [Git]
tags: [git]     # TAG names should always be lowercase
image:
  src: /assets/img/relax.jpg
  width: 640   # in pixels
  height: 427   # in pixels
  alt: relax, my friend.
---
So you've changed your project's `.gitignore` after accidentally uploading the config file containing the password you use for everything that isn't your online banking account.

You hurriedly create a new `git commit -m "changes"` and push. Huh? The secrets are still there!

Well, let me save you some grief! You need to **delete your tracked files cache**. Heres how:
- Run `git rm -r --cached .` to delete your cache
- Then `git add .` to re-add everything, but this time only the files not excluded by `.gitignore`
- Then `git commit -m "changes but for real this time!"` and push

You're welcome.

### Bonus tip
`git commit -am "your message here"` does the job of two lines! the `-am` flag tells Git to add all files to staging.