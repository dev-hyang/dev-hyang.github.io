---
layout:     post
title:      2020-08-30-MERN stack CP02 - Build A React CRUD App
subtitle:   Project Backend Setup with Express and Node.js
date:       2020-08-30
author:     BY Elon
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - MERN
    - React
    - CRUD
---
<strong>Note1</strong>:In Markdown, you can use empty row + tab space to make a code block. Markdown would auto wrap tab leading lines within &lt;pre&gt;&lt;code&gt;.<br/>
<strong>Note2</strong>: We would like a better way to organize our project files, a better hierarchical way/design architecture. This is where I find the reference ->[How To Organize File Structure](https://stackoverflow.com/questions/51126472/how-to-organise-file-structure-of-backend-and-frontend-in-mern)
## Set up Backend
Usually we could build a backend server with Node.js/Express, as well as set up MongoDB and connect to the database from our Node.js/Express server by the Mongoose library.

The backend will use HTTP methods(GET, POST) to cover below functionalities:
* Retrieve the complete list of available todo items by sending an HTTP GET request
* Retrieve a specific todo item with HTTP GET request with a specific todo item ID as an additional parameter 
* Create a new todo item in the database by HTTP POST
* Update a todo item in the database with HTTP POST/PUT?

## Initiat the back-end project
### Find a way to organize your mern project file structure better
As we are going to develop the backend for our todo mern project, I want the project file structure to be better organized so that I could quickly locate my components. There is a good [reference](https://stackoverflow.com/questions/51126472/how-to-organise-file-structure-of-backend-and-frontend-in-mern) as noted.
### Install Express, body-parser, CORS, and Mongoose
When we have our /backend folder, we enter it and use <code>$ npm init -y</code> to create a package.json file inside it. Then we could use <code>$ npm i express body-parser cors mongoose</code> to add dependecies in the server end. Let's take a closer look at the dependencies:
- <strong>express</strong>: Express is a fast and lightweight web framework for Node.js.
- <strong>body-parser</strong>: Node.js body parsing middleware
- <strong>cors</strong>: CORS is a node.js package for providing an Express middleware that can be used to enable CORS with various options. Cross-origin resource sharing (CORS) is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the first resource was served.
- <strong>mongoose</strong>: A Node.js framework interacts with mongoDB.

### Install Nodemon and Concurrently
In the /backend, we can use <code>$ install -i nodemon concurrently</code> to include these two important packages. Nodemon is a utility that will monitor for any changes in your source and auto restart your server. Concurrently is a npm package that allows you to run multiple commands concurrently.

### Create app.js file
In the /backend, we then create a app.js file and fill below contents in it:
	
	const express = require('express');
	const app = express();
	const bodyParser = require('body-parser');
	const cors = require('cors');
	const PORT = 4000;
	// attach the cors and body-parser middleware
	app.use(cors());
	app.use(bodyParser.json());
	// Make the server listening on PORT 4000
	app.listen(PORT, function(){
		console.log("Server is running on Port: " + PORT);
	});


## Install MongoDB
1. We need to check if MongoDB have already been installed. <code>$ which mongod</code> can help to do the check. If not installed, we could use <code>$ brew install mongodb</code> on MacOS.
2. After installed mongodb, we then create a data directory <code>$ mkdir -p /data/db</code> Before running mongod for the first time, check your permission for the directory. But after MacOS upgraded to Catalina in 2019. We could not use /data/db any longer in the root directory. Instead, just customized our data/db in any directory. Then each time,

### <code> $ brew services list</code>
This command helps to list all services on can be launched by brew.
For example:

	Name              Status  User Plist
	mongodb-community stopped

### <code> $ brew services start mongodb-community </code>
This command helps to start mongodb server

### <code> $ brew services stop mongodb-community </code>
This command helps to stop mongodb service.

### <code> $ mongo </code>
Enter mongodb control panel and CLT, we can use <code>show dbs</code> to check how many db on the mongodb server. You can also use <code>use todos</code> to create your own db. Other command in mongo shell could be found [here](https://docs.mongodb.com/manual/crud/)

### <code> $ mongod --dbpath /users/xxx/data/db</code>
After you installed your mongodb, each time add a dbpath paramter when run the command to check the database it uses.

## Connect MongoDB with mongoose
When choose the network PORT, you can use <code>$ sudo lsof -iTCP -sTCP:LISTEN -n -P</code> to check used ports

	const mongoose = require('mongoose');
	// Make the server listening on PORT 3002
	mongoose.connect('mongodb://127.0.0.1:27017/todos', {
		useNewUrlParser: true
	});
	const conn = mongoose.connection;
	conn.once('open', function(){
		console.log("MongoDB database is successfully connected.")
	});

## Implement the server endpoints
### Create a Schema in MongoDB

	const mongoose = require('mongoose');
	const Schema = mongoose.Schema;
	//Create the schema/table in mongoDB
	let Todo = new Schema({
		todo_description:{
			type: String
		},
		todo_responsible:{
			type: String
		},
		todo_priority:{
			type: String
		},
		todo_completed:{
			type: Boolean
		}
	});
	module.exports = mongoose.model('Todo', Todo);

### Update Server.js

	const express = require('express');
	const app = express();
	const bodyParser = require('body-parser');
	const cors = require('cors');
	const mongoose = require('mongoose');
	const PORT = 3002;
	// attach the cors and body-parser middleware
	app.use(cors());
	app.use(bodyParser.json());
	// Make the server listening on PORT 4000
	mongoose.connect('mongodb://127.0.0.1:27017/todos', {
		useNewUrlParser: true
	});
	const conn = mongoose.connection;
	conn.once('open', function(){
		console.log("MongoDB database is successfully connected.")
	});
	const todoRouter = require('./routes/todo.route');
	app.use('/todos', todoRouter)
	app.listen(PORT, function(){
		console.log("Server is running on Port: " + PORT);
	});
### Create Routers

	const router = require('express').Router();
	let Todo = require('../models/todo.model');
	//Get methods for all todo items
	router.route('/').get((req, res) => {
	  Todo.find()
	    .then(todos => res.json(todos))
	    .catch(err => res.status(400).json('Error: ' + err));
	});
	//find todo item based on specific ID
	router.route('/:id').get((req, res) => {
		let id = req.params.id;
		Todo.findById(id)
			.then(todo => res.json(todo))
			.catch(err => res.status(400).json('Error: ' + err));
	});
	//POST method to create new Todo item and add it in db
	router.route('/add').post((req, res) => {
		// console.log(req.body);
		let todo = new Todo(req.body);
		//save() method to save object into database
		// console.log(todo);
		todo.save()
			.then(todo => {
				res.status(200).json({'msg': 'todo added successfully!',
									'todo': todo,
									'req_body': req.body});
			})
			.catch(err => {
				res.status(400).send('adding new todo failed.');
			});
	});
	//Update, Path parameters /update/:id
	router.route('/update/:id').post((req, res) => {
		Todo.findById(req.params.id)
			.then(todo => {
				if (!todo)
					res.status(404).send("data is not found");
				else
					todo.todo_description = req.body.todo_description;
					todo.todo_responsible = req.body.todo_responsible;
					todo.todo_priority = req.body.todo_priority;
					todo.todo_completed = req.body.todo_completed;
					todo.save()
						.then(todo => {
							res.json('Todo updated!');
						})
						.catch(err => {
							res.status(400).send("Update not possible");
						})
			})
			.catch(err => {
				res.status(404).send("id is invalid.");
			});
		});
	module.exports = router;


## POSTMAN test server
### Issue #1 - Keep getting empty req.body
It is due to the body properties I set for the contents is raw-text or form-data, while it is required to be raw-json.

### Issue #2 - Misunderstand Path parameter with Query parameter
When testing GET /:id and Update /:id, we need to enter :id in the url, then POSTMAN will auto populate the path parameters for us.