---
layout:     post
title:      2020-09-20-MERN stack CP06 - Add Login AuthN/AuthZ
subtitle:   AuthN/AuthZ with Jsonwebtoken(JWT)
date:       2020-09-20
author:     BY Elon
header-img: img/post-bg-jwt.png
catalog: true
tags:
    - MERN
    - AuthN/AuthZ
    - JWT
---
[Github Repo](https://github.com/elon-hangyang/Login-Auth-App)
In the server/backend side, 
## Step1, Setup project.json file main entry as "server.js" instead of "index.js"
After <code>$ npm init</code>, there would be a project.json file in backend folder. Here you are going to modify the default main entry from index.js to server.js.

## Step2, install dependencies like jwt and passport
<code>$ npm i bcryptjs body-parser concurrently express is-empty jsonwebtoken mongoose passport passport-jwt validator</code>

* bcryptjs: to hash password before storing in the database
* body-parser: to parse request bodies content in a middleware
* concurrently: to run our backend and frontend concurrently and on different ports
* express: sits on top of Node to make the routing, request handling and responding easier to use
* is-empty: global function that will come in handy when we use validator
* jsonwebtoken: for authorization
* mongoose: to interact with NoSQL database - MongoDB Atlas version
* passport: to authenticate requests, which it does through an extensible set of plugins known as **strategies**
* passport-jwt: **passport** strategy for authenticating with a Json Web Token(JWT), lets you authenticate endpoints using a JWT
* validator: to validate inputs, (check for valid email format, confirming passwords match)

## Step3, install devDependency (-D)
<code>$ npm i -D nodemon</code> Nodemon is going to monitor your changes in your code and auto restart the server, which is very useful in development. Update the project.json to include:
	
	"scripts": {
		"start": "node server.js",
		"server": "nodemon server.js"
	}
later on, we can use <code>$ nodemon run server</code> to run our server.