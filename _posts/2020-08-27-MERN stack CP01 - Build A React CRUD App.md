---
layout:     post
title:      2020-08-27-MERN stack CP01 - Build A React CRUD App
subtitle:   Project Setup
date:       2020-08-27
author:     BY Elon
header-img: img/post-bg-2015.jpg
catalog: true
tags:
    - MERN
    - React
    - CRUD
---
## What's MERN stack?
- MERN stack is a set of full-stack techs. 
	+ **N**ode.js: Node.js is a JavaScript runtime built on Chrome's v8 JavaScript engine. Node.js brings JavaScript to the server.
	+ **M**ongeDB: A document-based open source database
	+ **E**xpress: A Fast, unopinionated, minimalist web framework for Node.js
	+ **R**eact: A JavaScript front-end library for building UI
MERN stack is very similar to MEAN stack where <strong>A</strong> stands for <q>Angular</q> instead of React.

## Set Up The React Application
1. <code>$ node -v</code> This is to check if Node.js is installed on your system;
2. <code>$ npx create-react-app mern_todo_app</code> <b>npx</b> command could allow us to execute create-react-app without installing it and create the initial React Project.
	- You might met some issues with <q>gyp</q> command or X-code, CLT issues. Just ignore them. You would get a new project directory mern_todo_app and it have a default React app with all dependencies installed.
	- How to push existing mern_todo_app directory to Github website?
		- Go to your Github profile ,create a repo named mern_todo_app and then copy the SSH root path
		- <code>$cd mern_todo_app</code>, use <code>$git remote -v</code> to check if there is already a remote repo on the cloud connected to current local repo. If not, then use <code>$git remote add origin {SSH remote address | HTTPS remote address}</code>

## Add Bootstrap To the React Project
We need to add Bootstrap framework to build UI with Bootstrap's CSS libraries. Rewrite the App.js files with below contents:
  import React, { Component } from "react";
	import "bootstrap/dist/css/bootstrap.min.css";

	class App extends Component {
		render(){

			return (
				<div className="container">
					<h2>MERN-Stack Todo App</h2>
				</div>
			);
		}
	}
	export default App;

## Set Up React Router
<code>$npm install react-router-dom</code> After install router package, we could add the routing configuration in App.js. Again, we rewrite our App.js file by below contents:
	import {BrowserRouter as Router, Route, Link } from "react-router-dom";
	import React, { Component } from "react";
	import "bootstrap/dist/css/bootstrap.min.css";

	class App extends Component {
		render(){

			return (
				<Router>
					<Route path="/" exact, component={Todolist} />
					<Route path="/edit/:id", component={EditTodo} />
					<Route path="/create", component={CreateTodo} />
					<div className="container">
						<h2>MERN-Stack Todo App</h2>
					</div>
				</Router>
			);
		}
	}
	export default App;

Among them, Route tag means new route to be added to the application. <q>path</q> and <q>component</q> attributes are used to configure connection between the paths/routes and components.

## Create Components
Store below three components in the new directly src/components
* todo_list.component.js
	import React, { Component } from 'react';
  export default class TodosList extends Component {
    render() {
        return (
            <div>
                <p>Welcome to Todos List Component!!</p>
            </div>
        )
    }
  }

* edit_todo.component.js
	import React, { Component } from 'react';
  export default class EditTodo extends Component {
    render() {
        return (
            <div>
                <p>Welcome to Edit Todo Component!!</p>
            </div>
        )
    }
  }

* create_todo.component.js

	import React, { Component } from 'react';
  export default class CreateTodo extends Component {
    render() {
        return (
            <div>
                <p>Welcome to Create Todo Component!!</p>
            </div>
        )
    }
  }

## Create basic layout and Navigation
We could extend bootstrap in the App.js file as following:
  
	import React, { Component } from "react";
  import { BrowserRouter as Router, Route, Link } from "react-router-dom";
  import "bootstrap/dist/css/bootstrap.min.css";
  import CreateTodo from "./components/create-todo.component";
  import EditTodo from "./components/edit-todo.component";
  import TodosList from "./components/todos-list.component";
  import logo from "./logo.svg";
  class App extends Component {
    render() {
      return (
        <Router>
          <div className="container">
            <nav className="navbar navbar-expand-lg navbar-light bg-light">
              <a class="navbar-brand" href="http://elonhangyang.com" target="_blank">
                <img src={logo} width="30" height="30" alt="elonhangyang.com" />
              </a>
              <Link to="/" className="navbar-brand">MERN-Stack Todo App</Link>
              <div className="collpase navbar-collapse">
                <ul className="navbar-nav mr-auto">
                  <li className="navbar-item">
                    <Link to="/" className="nav-link">Todos</Link>
                  </li>
                  <li className="navbar-item">
                    <Link to="/create" className="nav-link">Create Todo</Link>
                  </li>
                </ul>
              </div>
            </nav>
            <br/>
            <Route path="/" exact component={TodosList} />
            <Route path="/edit/:id" component={EditTodo} />
            <Route path="/create" component={CreateTodo} />
          </div>
        </Router>
      );
    }
  }
  export default App;

The navigation bar is displayed with two menu items included (Todos and Create Todo). By default the output of TodosList component is shown because it was connected to the default route of the application.