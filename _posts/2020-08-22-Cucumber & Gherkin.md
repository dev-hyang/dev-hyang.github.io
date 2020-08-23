---
layout:     post
title:      2020-08-22-Cucumber & Gherkin & Guzzle
subtitle:   Tools to support BDD
date:       2020-08-22
author:     BY Elon
header-img: img/post-bg-coffee.jpg
catalog: true
tags:
    - Web Development
    - PHP
    - Behavior Driven Development
---
* <h1> Cucumber </h1>
Cucumber is a tool to suport BDD. It reads executalbe specifications written in plain text and validates that the software does what the specifications say. The specification consists of multiple examples/scenarios. Each scenario is a list of steps for Cucumber to work thru. Cucubmer verifies the software conforms with the specification and generates a report indicating passed or failed cases.

* <h1> Gherkin </h1>
Gherkin is a set of grammar rules that makes plain text structured enough for Cucumber to understand. It serves:
	* unambiguous executable specification
	* automated testing using Cucumber
	* doc how the sys actually behaves
The Cucumber grammar exists in different spoken language(English, Franch, Spanish, etc). Gherkin docs are stored in .feature text files and are typically versioned in source control against the software.
	* *Step Definitions* connect Gherkin steps to programming codes. Steps in Gherkin --- {Step Definition} --- Systems

* <h1> Guzzle </h1>
Guzzle is an HTTP client built with and for PHP. The cURL software has typically handled how to process HTTP heavy lifting in PHP, or in some cases of quick hacking, the good old file_get_contents() function. Guzzle is a bit more advanced and simple at the same time. All complexity is hidden away in the class implementation. Usually we could install Guzzle with Composer. Guzzle allows your application to make HTTP requests. Guzzle can make HTTP requests to any device that is capable of sending an HTTP response, whether that be an API from twitter, facebook, or reddit, or any public website. 