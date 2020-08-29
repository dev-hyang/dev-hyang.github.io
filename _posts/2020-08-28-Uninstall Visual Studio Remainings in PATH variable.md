---
layout:     post
title:      2020-08-28-Uninstall Visual Studio Remainings in PATH variable
subtitle:   MacOS
date:       2020-08-28
author:     BY Elon
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - MacOS
    - PATH
    - Visual Studio
---
Today I got a question when I tried to use 
<code>$ for i in ${PATH//:/ }; do ls $i; done | sort | uniq | wc -l</code> to find how many commands there are in my MacOS system. However, it cast below issues:
<q>ls: /Users/dahang/anaconda3/bin /Users/dahang/.autojump/bin /usr/local/bin /usr/bin /bin /usr/sbin /sbin /usr/local/share/dotnet ~/.dotnet/tools /Users/dahang/flutter_dev/flutter/bin: No such file or directory 0</q>
It came to two odd directories in the path: 
- <code>/usr/local/share/dotnet</code>
- <code>~/.dotnet/tools</code>
The two directories were so odd that I could not find them anywhere in .zshrc or .bash_profile or .bash* files. However, if I entered command <code>$ echo $PATH</code> in the zsh, it executed successfully. There seemed nothing wrong with PATH. But why it prompted such an error still puzzles me.
So I googled it. What surprised me was that these two directories were said to be set by default when MacOS upgraded to Catelina OS. They stored in /etc/paths.d/. I just found them and the two tools were said to support .NET core commands.
- Other interesting reading about Command Line Tools:
[Use zsh as the default shell on your Mac](https://support.apple.com/en-us/HT208050)
[Power up your Terminal using Oh-my-Zsh + iTerm2](https://medium.com/swlh/power-up-your-terminal-using-oh-my-zsh-iterm2-c5a03f73a9fb)
