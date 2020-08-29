---
layout:     post
title:      2020-08-26-Set up SSH key/pair for Github
subtitle:   Github acct Config instead of using name/password in .config file
date:       2020-08-26
author:     BY Elon
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - Github
    - Git
    - SSH
---
- Based on Github support QAs, we have two pre-steps:
1. [Check for existing key](https://docs.github.com/en/enterprise/2.13/user/articles/checking-for-existing-ssh-keys)
2. [Generate new key](https://docs.github.com/en/enterprise/2.13/user/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
	- Remember when you type a command in terminal, don't use $ eval, use eval directly
3. [Working with SSH key passphrase](https://docs.github.com/en/enterprise/2.13/user/articles/working-with-ssh-key-passphrases)
4. [Add ssh key to Github account](https://docs.github.com/en/enterprise/2.13/user/articles/adding-a-new-ssh-key-to-your-github-account)
5. [Change a remote's URL](https://help.github.jp/enterprise/2.11/user/articles/changing-a-remote-s-url/)
6. [(Optional)Adding an existing project to GitHub using the command line](https://docs.github.com/en/github/importing-your-projects-to-github/adding-an-existing-project-to-github-using-the-command-line)
	- The first time to use SSH key, you might get below message:<q>The authenticity of host 'github.com (140.xx.xxx.x)' can't be established.
	RSA key fingerprint is SHA256:*****************.
	Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
	Warning: Permanently added 'github.com,140.xx.xxx.x' (RSA) to the list of known hosts.
	Enumerating objects: 39, done.
	Counting objects: 100% (39/39), done.
	Delta compression using up to 4 threads
	Compressing objects: 100% (39/39), done.
	Writing objects: 100% (39/39), 291.16 KiB | 5.49 MiB/s, done.
	Total 39 (delta 0), reused 0 (delta 0)</q>