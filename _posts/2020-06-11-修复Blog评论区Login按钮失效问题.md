---
layout:     post
title:      修复Blog评论区Login按钮失效问题
subtitle:   Fix the bug of invalid "Login with GitHub" button in the gitalk comment area
date:       2020-06-11
author:     Elon
header-img: img/post-bg-desk.jpg
catalog: true
tags:
    - github
    - gitalk
---

## How to setup your Gitalk with your personal blog

. The issue is "Redirect URI mismatch". We go to check [gitalk github.io](https://github.com/gitalk/gitalk) which tells us that we should have a valid "Authorization Callback URL". We did have, but it was the repository path. xx-name.github.io. 
. Then we go to the [GitHub OAuth App](https://github.com/settings/developers) where we update it to github.com official website. The gitalk login Github button works.
