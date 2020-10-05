---
layout:     post
title:      2020-09-02-Fixing Bug CP02 - Keep getting "undefined" when using process.env.XX_VARS in React App
subtitle:   How to set .ENV variables for MERN Project
date:       2020-09-02
author:     BY Elon
header-img: img/post-bg-BJJ.jpg
catalog: true
tags:
    - MERN
    - React
    - dotenv
---
Everyone knows that config is very important, especially in a front-back end project. Here is the key in a MERN project = **dotenv library + .env file**

## Install dotenv in the backend - Express + Node.js
Enter into our server directory from command line, then enter <code>$ npm i dotenv --save</code>. Then we add below statement in our App.js or server.js file before we use process.env.XX_VARS. Note there is no requirement/specification on the name of vars.

	require('dotenv').config();

After that we would put a .env file in our server root directory. Put all variables we want to use there, here is a sample:
	
	MERN_APP_ENDPOINT = http://localhost:3002/
	PORT = 3002
	MONGODB_URI = mongodb://127.0.0.1:27017/todos

## ## Install dotenv in the frontend - React
While 90% instructions are similar to those in the backend, there is a unique requirement in the frontend-React App. That is naming convention in the .env file must start with **REACT_APP_**. I cannot believe it until I got so many undefined in my console when testing. Thanks for [stackoverflow's reference](https://stackoverflow.com/questions/49579028/adding-an-env-file-to-react-project) and [create-react-app documentation](https://create-react-app.dev/docs/adding-custom-environment-variables/).