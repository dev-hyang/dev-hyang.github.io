---
layout:     post
title:      2020-08-09-RESTful Developer Path CP01
subtitle:   URL vs URI
date:       2020-08-09
author:     BY Elon
header-img: img/post-bg-coffee.jpg
catalog: true
tags:
    - Web Development
    - REST
    - API
---

## URL vs URI
URI = Universal Resouce Identifier, a compact sequence of characters that identifies an abstract or physical resource that provides a simple and extensible means for identifying a resource.

URL = Universal Resource Locator, subset of URI that identifies a resource and explains **how to access** that resource by providing an explicit method(protocol) like https:// or ftp://

URN = Universal Resource Name, rarely talk about. It's also subset of URI, but different from URL, more like a person name, while URL provides actual physical location.

## What's RESTful APIs?
HTTP-HyperText Transfer Protocol, is the protocol your web browser uses to access hypertext documents on the world wide web. While REST is a set of six software architecture design constraints/standard that produce a specific type of service. It's not saying that REST = HTTP or linked. Because you can also make a REST on FTP or SMTP. They are just convenient pairing. When REST runs on HTTP to access a web resource, we call it a RESTful API. The web platform is what makes it RESTful.

## Six constraints of REST
- ***Client-Server architecture***: client manages user interface concerns while server manages data storate concerns
- ***Statelessness***: no client context or information(aka, "state") can be stored on the server between requests. The client is responsible for keeping track of its own session state and all requests sent from a client must be *self-contained and complete*. If the client's session state is relevant, it must be sent along with a request and if the server needs to store that state, it must pass it on to a database or similar service for a specific time. As an example, the server can be asked to pass on an authentication token for a set period of time to allow authenticated r
- ***Cacheability***: All REST responses must be clearly marked as cacheable or not cacheable. 
- ***Layered System***: Client cannot know, and shouldn't care, whether it's connected directly to the server or to an intermediary like CDN or mirror.
- ***Code on demand***: Servers are allowed to transfer executable code like JavaScript and compiled components to clients
- ***Uniform interface***
	* <b>Resource identification in request</b>: The request must specify what response it is looking for and what format the response should be. Like data in db server would return as JSON, XML or HTML.
	* <b>Resource manipulation through representatives<b>: Access is granted uniformly once the client get the resource representative.
	* <b>self-descriptive messages<b>: Each representation must decribe its format.
	* <b>hypermedia as the engine of application state</b>: Once a client has access to a REST service, it should be able to discover all available resources and methods through the hyperlinks provided.

## Whos is REST clients?
A client is the device/web/app itself, not human. We are merely the operators of these clients. The beauty of the REST API is that it does not care who the client is as long as it follows the rules.

You provide an interface for your data to be quite literally consumed by whatever client comes knocking. That's not to say all REST APIs are completely open, or that anyone can do anything they want with the data in the REST API. Most REST APIs have strict limits on who can access what, which capabilities they are granted, and how many requests they can make in a set time period.

That is why we could use a web crawler to collect information from per website with authentication ID and PWD.

Some common tools for REST clients is Postman, Insomnia

## Discovery REST APIs
Thanks to HyperMedia Engine constraint. We could use OPTIONS to find all resources and methods in that REST APIs.

## Resource vs Representation
The key abstraction of information in REST is a resource. Any information that can be named can be a resource: a document, an image or a collection of other resources, etc. Resource is a conceptual mapping to a set of entities, not the entity itself. A representation of a resource is a unique copy of that resource, not the resource itself. That's why different people can get resource at the same time in different format because representation could be displayed in different format.

## Methods(verbs) - HTTP methods often
- GET - retrieve the specified resource from server. If succeed, it returns 200 OK. O.W., it returns 404 Not Found.
- POST - create a new resource and add it to a collection. If succeed, it return 201 Created. O.W., 
	* 401 Unauthorized(No authorization) 
	* or 409 Conflict(already existed) 
	* or 404 Not Found(the main resource collection doesn't exist).
- PUT - update an existing singleton resource based on ID by replacing content. If no resource found in the REST server, it might create a new resource with specified ID. If succeed, returns 200 OK, O.W., 
	* 401 Unauthorized, 
	* or 204 No Content, if not content is present at server.
	* or 404 Not Found (if ID is not found)
	* or 405 Method Not Allowed.(if put is applied to a collection resource)
- PATCH - modify an existing singleton resource based on ID without replacing everything as PUT does. It returns the same as PUT.
- Delete - can only be used on singleton resource based on ID.
- OPTIONS - get the options available from the resource
- HEAD - get only the response head session from the resource.

## HTTP status code
- 1xx: information
- 2xx: success
	- 200 OK
	- 201 Created
	- 204 No Content
- 3xx: Redirection
	- 301 Moved Permanently
	- 302/303 Found at this other URL
	- 307 Temporary redirect (confusing)
	- 308 Resume incomplete (confusing)
- 4xx: Client error
	- 400 Bad request, either request is malformed or too large or similar
	- 401 Unauthorized, lack proper authorization to access the resource
	- 403 Forbidden, request is refused by server usually caused by not loggin or not have correct permission
	- 404 Not Found, desired resource does not exist
	- 405 Method not allowed, like using POST on a resource which only has GET method.
- 5xx: Server error
	- 500 Internal server error
	- 502 Bad gateway
	- 503 Service unavailable, common when server is overloaded

## Authentication/Authorization
The response and methods you can apply on a resource depends heavily on the authorization level you are assigned.