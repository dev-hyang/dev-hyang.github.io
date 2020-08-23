---
layout:     post
title:      2020-08-21-Testing and Validating RESTful APIs
subtitle:   RESTful Developer Path 04
date:       2020-08-21
author:     BY Elon
header-img: img/post-bg-coffee.jpg
catalog: true
tags:
    - Web Development
    - REST
    - API
---
1. Introduction
	* Target API: Github V3, https://developer.github.com/v3/, free to use, 
	* Required Tools: PHP 7.x, Your favorite text editor, HTTP request library(probably Guzzle), Behat 3.x
	* Useful Tools: Xdebug, Postman, Runscope
2. Understand Behavior Testing with [Gherkin]()
	* [Behavior-Driven Development - BDD](), BDD is a second-generation, outside-in pull-based multiple-stakeholder, multiple-scale, and high-automation agile methodology.
	* BDD validates "working" software based on the external behavior of the system, preferably in an automation fashion.
	* BDD User Case in Gherkin Syntax, Given (xx condition), When (xx action), Then (xx result), And (xx).
3. By using double quotes or numeric numbers, we could declare a variable in our Gherkin feature file. PHP uses period " . " to concatenate strings.
4. Types of AuthZ Options
	* ***Username and Password***, can be your account name and password, but not always; usually HTTP basic authentication, like https://username:password@api..
	* ***API keys/tokens***, Long random string separate from account credentials, like https://api.test.com?key=mytestkey. Be careful not to expose your key in unsafe network.
	* ***OAuth***, OAuth2.0 handles authZ outside the API exchange. Retrieves an access token and (often) a refresh token.
5. Exercises could be found [here](https://github.com/elon-hangyang/TestingRestfulAPI).