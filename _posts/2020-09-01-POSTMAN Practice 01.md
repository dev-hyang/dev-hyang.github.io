---
layout:     post
title:      2020-09-01-POSTMAN Practice 01
subtitle:   How to test /:id path params
date:       2020-09-01
author:     BY Elon
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - Web Development
    - REST
    - API
---
When talking about path params and query params, it usually makes me feel confusing. There is a documentation in POSTMAN community which helps me to understand and test them separately.

## Path params like /:id
Path parameters form part of the request URL, and are referenced using placeholders preceded by : as in the following example: /user/:id

To send a path parameter, enter the parameter name into the URL field, after a colon. When you enter a path parameter, the POSTMAN will populate it in the Params tab, where you can also edit it.

## Query params like /?id=
Query parameters are appended to the end of the request URL, following ? and listed in key value pairs, separated by & using the following syntax: ?id=1&type=new

To send a query param, add it directly to the URL or open Params and enter the key-value pair. Params are not auto url encoded, you can right-click selected text, and choose EncodeURLComponent to manually encode a param value