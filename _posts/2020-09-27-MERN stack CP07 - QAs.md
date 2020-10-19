---
layout:     post
title:      2020-09-27-MERN stack CP07 - QAs
subtitle:   QAs
date:       2020-09-27
author:     BY Elon
header-img: img/post-bg-jwt.png
catalog: true
tags:
    - MERN
---
# How to store a field representing the time of the day, like 3:30?
It does not need to be a fully qualified timestamp because the date is irrelevant.

[Ans](https://stackoverflow.com/questions/20473765/best-way-to-store-time-of-day-in-mongoose):
I'd suggest storing it either as seconds since midnight (as a Number) or as a padded numeric String stored in 24 hour format.

For example, 3:30PM:

Seconds (stored as a number): 55800
String: "1530" (always must be 24 hour format with a leading numeric digit to have the same number of places, so 8:30AM would be "0830"
Both can be sorted, indexed, queried by range. Both take approximately the same number of bytes. Since neither is very human friendly readable, you'd probably need to format them either way for display. It's really up to you which one would work better for your use.

# How to Fix 401-Unauthorized error when testing API on POSTMAN
Find the api -> Check the auth tab in the request page, in my case, it is jwt(json-web-token), so choose type "Bearer Token", and you can use /login API to generate a new token for yourself. Paste the token content from the response data int he Token field below "Bearer Token". Try to test the API again.