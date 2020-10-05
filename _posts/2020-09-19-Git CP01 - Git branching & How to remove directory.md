---
layout:     post
title:      2020-09-19-Git CP01 - Git branching & How to remove directory
subtitle:   
date:       2020-09-19
author:     Elon
header-img: img/post-bg-desk.jpg
catalog: true
tags:
    - Git
    - Version Control
---
## Git Branching
Before we enter the zone, let's introduce some terms in SDE.
#### [What's hotfix?](https://baike.baidu.com/item/hotfix).
A hotfix, is a software patch that is applied to “hot” (aka live) systems. For us developers, this usually means that it’s a change that was made quickly and outside of the normal development processes, as an urgent measure against certain issues that need to be fix immediately.

#### [Patch vs Hotfix]()
A patch is a program that makes changes to software installed on a computer. Software companies issue patches to fix bugs in their programs, address security problems, or add functionality. ... Sometimes, a hotfix refers to a patch that can be applied without downtime or restarting the system

### [Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
Here is a Scenario:

* 1, do some work on a website
* 2, create a branch for a new user story you are working on
* 3, do some work in that branch

At this stage, you'll receive a call that another issue is critical and you need a hotfix. You will do:

* 1, Switch to your production branch
* 2, Create a branch to add the hotfix
* 3, After it's tested, merge the hotfix branch, and push to production
* 4, Switch back to your original user story and continue working

To create a new branch and switch to it at the same time, you can run the git checkout command with the -b switch:
	
	$ git checkout -b iss53
	Switched to a new branch "iss53"

You work on your website and do some commits. Doing so moves the iss53 branch forward, because you have it checked out (that is, your HEAD is pointing to it).

## How to remove directory from git and local

	git rm -r directories // This deletes from filesystem
	git commit . -m "directory removed"
	git push origin <git-branch> (usually 'master', but not always)

## How to remove directory from local
	
	git rm -r --cached myFolder
	git commit -m "remove from remote git repo"
	git push origin <git-branch>