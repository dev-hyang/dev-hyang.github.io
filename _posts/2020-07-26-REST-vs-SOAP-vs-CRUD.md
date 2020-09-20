---
layout:     post
title:      2020-07-26-REST-vs-SOAP-vs-CRUD
subtitle:   Basics
date:       2020-07-26
author:     Elon
header-img: img/post-bg-desk.jpg
catalog: true
tags:
    - HTTP
    - REST
    - SOAP
    - CRUD
---

## What's [REST](https://restfulapi.net/)?
REST - *RE*presentational *S*tate *T*ransfer, it is an architectural style. It is for exposing Public APIs to handle CRUD operations on database. REST is focusing on accessing named resources through a single consistent interface.

A truly RESTful path should only contain nouns - the HTTP methods (GET / POST /PUT /DELETE /HEAD /TRACE) used on the endpoint should determine the action. For example:
- POST /users/{id}
- GET /users/{id}
- PATCH /users/{id}
- DELETE /users/{id}
- PUT /users/{id}
instead of:
- GET /users/search
- GET /users/delete
HEAD is similar to GET


## What's SOAP?
A protocol.

## What's CRUD?
Create/Read(Retrieve)/Update/Delete on database management operations.

## REST vs SOAP
### REST Characteristics:
- Since REST uses standard HTTP it is much simpler in just about every way.
- REST is easier to implement, requires less bandwidth and resources.
- REST permits many different data formats where as SOAP only permits XML.
- REST allows better support for browser clients due to its support for JSON.
- REST has better performance and scalability. REST reads can be cached, SOAP based reads cannot be cached.
- If security is not a major concern and we have limited resources. Or we want to create an API that will be easily used by other developers publicly then we should go with REST.
- If we need Stateless CRUD operations then go with REST.
REST is commonly used in social media, web chat, mobile services and Public APIs like Google Maps.

### SOAP Characteristics:
- SOAP is not very easy to implement and requires more bandwidth and resources.
- SOAP message request is processed slower as compared to REST and it does not use web caching mechanism.
- WS-Security: While SOAP supports SSL (just like REST) it also supports WS-Security which adds some enterprise security features.
- WS-AtomicTransaction: Need ACID Transactions over a service, you’re going to need SOAP.
- WS-ReliableMessaging: If your application needs Asynchronous processing and a guaranteed level of reliability and security. REST doesn’t have a standard messaging system and expects clients to deal with communication failures by retrying.
- If the security is a major concern and the resources are not limited then we should use SOAP web services. Like if we are creating a web service for payment gateways, financial and telecommunication related work then we should go with SOAP as here high security is needed.

## REST vs CRUD