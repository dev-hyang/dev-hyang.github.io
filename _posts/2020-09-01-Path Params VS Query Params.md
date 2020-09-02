---
layout:     post
title:      2020-09-01-Path Params VS Query Params
subtitle:   RESTful API
date:       2020-09-01
author:     BY Elon
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - Web Development
    - REST
    - API
---
## Best Practices
Best practice for RESTful API design is that path params are used to identify a specific resource or resources, while query parameters are used to sort/filter those resources.

As far as syntax is concerned, your URL names should be all lowercase. If you have an entity name that is generally two words in English, you would use a hyphen to separate the words, not camel case.

A good reference to go is here -> [When do I use path params vs. query params in a RESTful API?](https://stackoverflow.com/questions/30967822/when-do-i-use-path-params-vs-query-params-in-a-restful-api)