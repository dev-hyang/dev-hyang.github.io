---
layout:     post
title:      2020-08-13-What is CDN and how it work?
subtitle:   RESTful Developer Path 01
date:       2020-08-13
author:     BY Elon
header-img: img/post-bg-desk.jpg
catalog: true
tags:
    - Web Development
    - REST
    - API
---
<pre>
<q>A CDN(Content Delivery Network) is a highly-distributed platform of servers that helps minimize delays in loading web page content by reducing the physical distance between the server and the user.

Without CDN, content origin servers must respond to single end user request. This result in significant traffic to the origin and subsequent load, thereby increasing the chances for origin failure if the traffice spikes are exceedingly high or if the load is persistent.
<cite>Akamai.com</cite>
</q>
<strong>The goal of CDN is to reduce latency - the delay between submitting a request for a web page and the web page fully loading on your device - by reducing the physical distance that the request has to travel.
</strong>
</pre>
For example, if you are in Europe and send a request to retrieve content located in US. You probably will not want to go through the whole Atlantic ocean to get the website content. Instead, CDN would store a cached version of website contents on multi-geographical locations around the world, which is known as "Points of presence"(PoPs). For most CDNs, each request would cause the end user to be mapped to an optimally-located CDN server and the server will respond with the cached (pre-saved) version of the requested files. If it fails to get the files, it first goes to other servers in CDN platform. When content is unavailable or stale, the CDN will act as a request proxy to the origin server and store the fetched content to serve future requests.