---
layout:     post
title:      2020-08-17-Designing RESTful APIs
subtitle:   RESTful Developer Path 03
date:       2020-08-17
author:     BY Elon
header-img: img/post-bg-coffee.jpg
catalog: true
tags:
    - Web Development
    - REST
    - API
---
1. API Design Must Be delibrate.
	- Decide what functionality to expose
	- Decide how to expose it
	- Decide the best way to expose it
	- Test and (in)validate assumptions
	- Repeat
2. Affordances
Something which allows you to perform an action or accomplish a goal.
	* What the API does
	* What the API makes easy
	* What the user wants to do
3. Approaches to add an API
	1. ***Bolt-On strategy*** for existing system to add an API after facts. 
		- Pros: It is seen as brute-force way but is generally the fastest way to get something useful. It also takes use of existing code and system.
		- Cons: Poor architecture decisions and bad name conventions tend to seep/leak thru the API which causes problems to external interfaces
	2. ***Greenfield Strategy*** for new systems which you have complete freedom and flexibility
		- Pros: Generally the "API first" or "Mobile First" mindset, the easiest way to develop an API. It can take advantage of new techs and architectures and possibly reinvigorates the team
		- Cons: it tends to be the hardest option because it often requires massive upfront investment before any benefits apprear.
	3. ***Facade Strategy*** for replacing systems piece by piece.
		- Pros: Ideal for legacy systems as the application is always functional.
		- Cons: can be challenging to have "multiple mindsets" in the system; can be hard to replicate behavior for a full 1:1 conversion.
4. Three quick tips on Modeling API
	1. ***Don't worry about the tools***, either NoteCards, Post-it notes or Kanban works.
	2. ***Have a consistent process***, to document things in the same way and same steps, you can reduce the likehood to miss something.
	3. ***It doesn't count unless it's written down***, Document everything - your assumptions, decisions, deferred tasks, and anything else that might be important to you, your team or your customers in six months.
5. The Modeling Process
	1. Identify participants, Also known as the people who will use our API, or better - the entities who will use our API. But be careful of your system boundaries! Clearly identify what you are responsible for and what are other, even third-party, components.
	2. Identify activities, you should include all the participants, not just yourself.
	3. Break into steps
		For example, identify participants and activities to order a book online.
		* who are our participants? customer, online book store manager
		* What are activities? 
			1. The customer searches for a book
			2. The customer adds the book to their cart
			3. The customer adds more things? remove things?
			4. The customer checks out
			5. The stock clerk retrieves and ships the book
			6. Customer support contacts the customer about the book
		* Remember Document Gaps!!! Every specification has gaps, ambiguities, and incomplete stories. Instead of guessing, ask the product owner.
	4. Create API definition
		* Identify the Resources. -- Find the Nouns.
			- Items, list items/view items/
			- Cart, Add item to cart/View cart/Check out
			- Orders, list orders/View orders/Cancel orders
			- Login/Logout What about customers?
		* Mapping activities to Methods/Verbs and actions using HTTP verbs. GET/DELETE/PUT/POST
		* Types of relationship
			- Independent, can exist on its own without any other resources
			- Dependent, can only exist if another resource already exist.
			- Associative, can be dependent or independent but needs additional infor to describe it.
		* Items are independent, Carts are dependent on Items, Orders are dependent on Carts, Orders must have customers. This is not the common case. It is also not a good way to design your API to expose your DB design.
	5. Validate your API
		* Review your listed steps on note card, peer review/team review to find out anying missing if possible. Then can try writing code, but not code for API. We don't care if the codes can compile.
		* Use a MicroFramework
			- Use hapi.js for Node, Sinatra for Ruby, Slim or Silex in PHP
			- Accept incoming requests
			- Validate verbs and URL patterns
			- Return static HTTP response codes and payloads
		* Write the Documentation - Act as if the API exists
			- List the end points - describe what they do
			- List the parameters - describe what they mean
			- List the response codes - describe under when you get each
			- Show the response payloads - define the fields
		* Our goal is to get feedbacks from team members, product owners, partners. Be careful: 
			- The documentation should not be perfect.
			- Don't let the people to think the project is done.
			Good news is that you have a rough draft documentation.
6. Common Design Challenges
	1. Authentication and Authorization (AuthN & AuthZ), AuthN is not AuthZ. AuthN is who you are. AuthZ is what you can do.
		- What Authorization can depend on?
			* Who you are
			* Your group membership
			* Subscription level
			* Context (time of day, location, device)
			* Actions attempted (esp. for MFA)
		- API Keys
			* Benefits
				* Framework and programming language agnostic
				* Easy to add as a header or even to URL
			* Drawbacks
				* URLs are convenient but logger everywhere(not safe)
				* Not easy to update/rotate if compromised
		- Create your own AuthN/AuthZ protocol. (Don't do that)
		- OAuth 2.0 (Quite Common protocol)
			* Benefits
				* Reliable and well established
				* Massive ecosystem
				* Open-source and commercial options
			* Drawbacks
				* Complicated and not easy to implement the first time
			* More on Web Security: OAuth and OpenID Connect
	2. API Versioning
		Biased towards clarity of purpose and ease of use.
		- Versioning via Accept Header
			* Content negotiation, 
				* Establish the markup/notation(usually XML or JSON);
				* Can establish the media type (structure of the markup);
				* Can establish the version of the media type (and resource);
		- Versioning via URL
			* Clear and Explicit
			* Nothing is lost when you copy and paste
		- key is consistency. Either Accept Header (more proper)/ URL(easier) works, we should keep consistency by using same method.
	3. Content Types and Media Types
		- Name/Value Pairs are fine. But it's hard to extend.
		- Media Types
			1. Collection + JSON
				* Designed by Mike Amundsen
				* Designed specifically to deal with groups or collections of resources
				* Can also represent single items as a set of one
				* In use and some helper libraries and examples
			2. Hypertext Application Language (HAL)
				* Led by Mike Kelly
				* Separates the payload into two parts - data and links
				* Can also represent single items as a set of one
				* Growing use and some helper libraries and examples
				* --- Drawbacks ---
				* Can be verbose (it's okay)
				* Having metadata in links separate from data is odd - easy to lose context and not explore as appropriate
			3. Others: THe Ion Hypermedia Type, Siren, OData, JSON-LD, JSONAPI, Mason, UBER, Atom
	4. What's Hypermedia?
		* Hypermedia = Hyper + Media
			* Hyper means THe media is not linear - begining, middle, end don't necessarily mean anything int his context. Just like shopping in Amazon, either you enter in front page or product page, it's up to you.
			Like : Get https://api.github.com, the API can give us information and the options that are available from the context of where we are and what we are doing at any given time.
			Hypermedia in many APIs, like Github, Twilio, Okta, and many others.
	5. Content negotiation and caching
		* Content Negotiation, the mechanisms which allow different versions of the same document to exist at a single URL so the client-server can determine which version best fits their capabilities. This is like API versioning.
		* Caching, A way of storing and retrieving data so that future requests can retrieve it faster without performing an operation (calculation, network request, etc.) again
	6. Documentation
		* Donts
			- No PDF - could arise multi-version floating around issue. A Google Site or Other password protected tool is proper to use.
			- If you are using a CMS that doesn't show the end user's page history and/or versioning information.
		* Goals
			- need code snippet friendly
			- need page history, specifically user facing
			- need something easy to update
			- Searchable - if we cant find it, it doesn't exist.
			Drawback might be just two states (Updated or not), no workflow or staing space in most systems.
		* Samples like Jekyll - Ruby based
		* Current tools - Slate
	7. SDKs
		* Sometimes, a HTTP library and a JSON library are enough
		* O.W., SPOIL might be a good SDKs tool, 
			* Succinct, concise but precise - SDKs should encourage users to write less code
			* Purposeful, apply the same care and thought to SDKs as you would to documentation and API
			* Open Source, SDKs won't solve every problem every time - we should encourage wrappers, extensions, and use contributions.
			* Idiomatic, SDKs should use the patterns and conventions of the language they are designed for
			* Logical, SDKs should be consistent so lessons learned or common patterns are repeated elsewhere
			Choose Wisely - Based on your desired users
			Others : mca blog, Mike Amundsen, API Strategy & Practices conference, REST Fest

