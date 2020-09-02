---
layout:     post
title:      2020-08-31-Fixing Bug CP01 - Keep Getting Error while use mkdir /data/db on MacOS Catalina
subtitle:   
date:       2020-08-12
author:     BY Elon
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - MacOS
    - Mongodb
---
<b>Note</b>: [Stackoverflow Discussions](https://stackoverflow.com/questions/58034955/read-only-file-system-when-attempting-mkdir-data-db-on-mac)
<br /><b>Note</b>: [Medium BLog](https://medium.com/@bryantjiminson/fixing-data-db-not-found-error-in-macos-x-when-starting-mongodb-d7b82abb2479)
### The Upgrade of MacOS to Catalina brings side effect on MongoDB
If you have Mac and updated to Catalina than the root folder is no longer writable. If you try to enter <code>$ mongod</code> to manually start mongodb on your MacOS, you would keep getting the error: no directory /data/db found. 

To fix the issue, you can manually start it <code> $ mongod --dbpath={your customized db path}</code>. You could also manually start mongodb by <code>$ mongodb --config /usr/local/etc/mongod.conf</code>. A better way to ignore setting --dbpath or --config each time is to make alias in either .bashrc or .zshrc file on your MacOS as below.
<code>alias mongod='mongod --dbpath={your db path}'</code>
