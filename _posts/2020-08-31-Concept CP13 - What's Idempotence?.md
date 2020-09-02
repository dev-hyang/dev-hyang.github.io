---
layout:     post
title:      2020-08-31-Concept CP13 - What's Idempotence?
subtitle:   Idempotence in RESTful API
date:       2020-08-30
author:     BY Elon
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - RESTful APIs
---
幂等（idempotent、idempotence）是一个数学与计算机学概念，常见于抽象代数中。 在编程中一个幂等操作的特点是其任意多次执行所产生的影响均与一次执行的影响相同。 幂等函数，或幂等方法，是指可以使用相同参数重复执行，并能获得相同结果的函数。

From a RESTful service viewpoint, for an operation (or service call) to be idempotent, clients can make the same call repeatedly while producing the same result. AKA< making multiple same requests has the same effect as making a single request. 

The PUT and DELETE methods are defined to be idempotent. However, there is a caveat on DELETE. The problem with DELETE, which if successful would normally return 200(ok) or 204(No content), will often return a 404(Not found) on subsequent calls, unless the service is configured to "mark" resources for deletion without actually deleting them.

GET, HEAD, OPTIONS and TRACE methods are idempotent.

POST is not idempotent because it's used to create stuff. Each time it would create a different instance.
