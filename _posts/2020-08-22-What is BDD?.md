---
layout:     post
title:      2020-08-22-What is BDD?
subtitle:   To reduce the gab between BAs and Developers
date:       2020-08-22
author:     BY Elon
header-img: img/post-bg-coffee.jpg
catalog: true
tags:
    - Web Development
    - PHP
    - Behavior Driven Development
---
* <h1>Behavior Driven Development</h1>
	* According to the introduction from [Cucumber.io](https://cucumber.io/docs/bdd/) <q>BDD is a way for software teams to work that closes the gab between BAs and Developers by: 
		+ 1) encouraging collaboration across roles to build shared understanding of the problem to be solved; 
		+ 2) working in rapid, small iterations to increase feedback and the flow of value; 
		+ 3) Producing system documentation that is automatically checked against the system's behaviors.
	</q>

	* BDD is seen as a set of plugins to existing agile process, to make it more timely and reliable. BDD encourages working in rapid iterations, continuously breaking down your users' problem into small pieces that can follow thru process ASAP.

	* Day-To-Day BDD is a 3-Step, iterative process:
		1. *Discovery*: Take a small upcoming change to the system - a ***User Story*** - and talk about concrete examples of the new functionality to explore, discover and agree on the details of what's expected to be done;
		2. *Formulation*: Document all those examples in a way that can be automated, and check for agreement;
		3. *Automation*: Implemented behavior described by each documented example, starting with an automated test to guide the development of code.
	* The idea is to make each change small and iterate rapidly, moving back up a level each time you need more information. Each time you automate and implement a new example, you’ve added something valuable to your system, and you’re ready to respond to feedback.
	
	* <h3>Discovery - what it could do</h3>
		By using structured conversations, called **discovery workshops**, that focus around real-world examples of the system from the users’ perspective. These conversations grow our team’s shared understanding of the needs of our users, of the rules that govern how the system should function, and of the scope of what needs to be done.<br>
		The scrutiny of a discovery session often reveals low-priority functionality that can be deferred from the scope of a user story, helping the team to work in smaller increments, improving their flow.
	* <h3>Formulation - What it should do</h3>
		As soon as we have identified at least one valuable example from our discovery sessions, we can now formulate each example as structured documentation. This gives us a quick way to confirm that we really do have a shared understanding of what to build. In contract to tranditional documentation, we use Gherkin to write documentation.
	* <h3>Automation - What it acutally dose</h3>
		Taking one example at a time, we automate it by connecting it to the system as a test. The test fails because we have not implemented the behaviour it describes yet. Now we develop the implementation code, using lower-level examples of the behaviour of internal system components to guide us as required.<br>
		When we need to come back and maintain the system later, the automated examples will help us to understand what the system is currently doing, and to make changes safely without unintentionally breaking anything. <br>
		This rapid, repeatable feedback reduces the burden of manual regression testing, freeing people up to do more interesting work, like exploratory testing.
