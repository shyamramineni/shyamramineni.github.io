---
title: "Personal Website Technical Update"
date: 2018-03-08T19:30:59+05:30
draft: false
---

Today I was able to get this website up based on GitHub based workflow. 
I commit content markdown into GitHub. I manually fire AWS codebuild and 
it picks up the source code of hugo project, runs Hugo and updates S3 bucket 
with static HTML from which this website is being served.

#Things TODO

1. Automate build based GitHub pull request
2. Figure out images
3. Organize content by Tags and Categories
4. Create pages