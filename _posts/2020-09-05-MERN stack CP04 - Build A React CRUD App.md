---
layout:     post
title:      2020-09-05-MERN stack CP04 - Build A React CRUD App
subtitle:   How to Update/Delete a todo item
date:       2020-09-05
author:     BY Elon
header-img: img/post-bg-BJJ.jpg
catalog: true
tags:
    - MERN
    - React
    - Express
    - MongoDB
    - Node.js
    - CRUD
    - REST
---
In last three sections, we discussed how to start up a MERN app, how to connect the app with Mongoose, how to bridge the frontend to backend, how to create a item. In this chapter, we are going to talk about how to update an item and delete an item.
## Update a todo item
In order to update the item, we need to modify the backend router to add a /update/:id route in todo.route.js file.

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
				//
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

In the frontend, we update the edit_todo.component.js as below:
	
	import React, { Component } from 'react';
	//import axios to connect backend to frontend
	import axios from 'axios';
	Expressort default class EditTodo extends Component {
	//
	//Add a constructor and initialize this.state with a hashMap
	constructor(props){
		super(props);
		/** set methods for this.state's properties: todo_description, 
		* todo_responsible, todo_priority
		*/
		this.onChangeTodoDescription = 
		this.onChangeTodoDescription.bind(this);
		this.onChangeTodoResponsible = 
		this.onChangeTodoResponsible.bind(this);
		this.onChangeTodoPriority = 
		this.onChangeTodoPriority.bind(this);
		//onSubmit method is used to handle the submit event of the form to create a new todo item
		this.onSubmit = this.onSubmit.bind(this);
		//
		this.state = {
			todo_description: '',
			todo_responsible: '',
			todo_priority: '',
			todo_completed: false
		}
	}
	//Set fields event Listeners
	onChangeTodoDescription(e) {
        this.setState({
            todo_description: e.target.value
        });
    }
    onChangeTodoResponsible(e) {
        this.setState({
            todo_responsible: e.target.value
        });
    }
    onChangeTodoPriority(e) {
        this.setState({
            todo_priority: e.target.value
        });
    }
    onChangeTodoCompleted(e) {
        this.setState({
            todo_completed: !this.state.todo_completed
        });
    }
	//componentDidMount() + this.props.match.params.id
	//ComponentDidMount() life method is to execute after first render() initialize
	componentDidMount(){
		//Retrieve the todo item from database based on id
		axios.get('/todos/'+this.props.match.params.id)
			.then(response => {
				this.setState({
					todo_description: response.data.todo_description,
					todo_responsible: response.data.todo_responsible,
					todo_priority: response.data.todo_priority,
					todo_completed: response.data.todo_completed
				})
			})
			.catch(err => console.log(err))
	}
	//Handle of onSubmit event in the form
	onSubmit(e){
		//we use preventDefault() method to ensure the default HTML form submit
		//behavior is prevented during test because the backend is not completed yet.
		e.preventDefault();
		//create a updated Todo item
		const updatedTodo = {
			todo_description: this.state.todo_description,
            todo_responsible: this.state.todo_responsible,
            todo_priority: this.state.todo_priority,
            todo_completed: this.state.todo_completed
		};
		//
		axios.post('/todos/update/'+this.props.match.params.id, updatedTodo)
		.then(res => console.log(res.data));
		//redirects user back to the todo list page
		this.props.history.push('/');
		//Refresh page
		window.location.reload();
		return false;
	}
	//Use JSX code to allows us put HTML into JavaScript
    render() {
        return (
            <div>
            	<h3 align="center">Update Todo</h3>
            	<form onSubmit={this.onSubmit}>
            		<div className="form-group">
            			<label>Description:</label>
            			<input type="text"
            					className="form-control"
            					value={this.state.todo_description}
            					onChange={this.onChangeTodoDescription}
            					/>
            		</div>
            		<div className="form-group">
            			<label>Responsible:</label>
            			<input type="text"
            					className="form-control"
            					value={this.state.todo_responsible}
            					onChange={this.onChangeTodoResponsible}
            					/>
            		</div>
            		<div className="form-group">
            			<div className="form-check form-check-inline">
            				<input className="form-check-input"
            						type="radio"
            						name="priorityOptions"
            						id="priorityLow"
            						value="Low"
            						checked={this.state.todo_priority === 'Low'}
            						onChange={this.onChangeTodoPriority}
            						/>
            				<label className="form-check-label">Low</label>
            			</div>
            			<div className="form-check form-check-inline">
            				<input className="form-check-input"
            						type="radio"
            						name="priorityOptions"
            						id="priorityMedium"
            						value="Medium"
            						checked={this.state.todo_priority === 'Medium'}
            						onChange={this.onChangeTodoPriority}
            						/>
            				<label className="form-check-label">Medium</label>
            			</div>
            			<div className="form-check form-check-inline">
            				<input className="form-check-input"
            						type="radio"
            						name="priorityOptions"
            						id="priorityHigh"
            						value="High"
            						checked={this.state.todo_priority === 'High'}
            						onChange={this.onChangeTodoPriority}
            						/>
            				<label className="form-check-label">High</label>
            			</div>
            		</div>
            		<div className="form-check">
            			<input className="form-check-input"
            				id="completedCheckbox"
            				type="checkbox"
            				name="completedCheckbox"
            				onChange={this.onChangeTodoCompleted}
            				checked={this.state.todo_completed}
            				value={this.state.todo_completed}
            				/>
            			<label className="form-check-label" htmlFor="completedCheckbox">
            			Complete</label>
            		</div>
            		//
            		<br />
            		//
            		<div className="form-group">
            			<input type="submit" value="Update Todo" className="btn btn-primary" />
            		</div>
            	</form>
            </div>
        )
    }
	}

From above file, there are two functions that we should pay attention to.
* this.props.history.push('/'), this function will redirects browser to previous '/' index page.
* window.location.reload(), will refresh the web page.

## [Delete a todo item](https://www.positronx.io/react-js/)
If we want to delete an item, then we need to add a new route in the todo.route.js file as below:

	//Use post or get or delete?
	//If you use delete, then delete will directly remove the record/doc from database
	//if you use post, then you can mark the doc as "Deleted" status
	router.route('/delete/:id').delete((req, res) => {
		Todo.findByIdAndRemove(req.params.id, (err, data) => {
			if (!err){
				res.redirect('/todos/');
			}
			else{
				console.log('Err when deleting todo:'+err);
			}
		});
	});

How would you schedule the frontend then, can you delete it directly in the todo list page? Or do it in the way which we update the record. Both will work.

### Delete in the Todo List page
If we want to delete it directly from the todo list page, todo.route.js is okay. But we need to rewrite the todo_list.component.js as below:

	import React, { Component } from 'react';
	import axios from 'axios';
	import TodoRow from './todoRow.component';
	//用一个tableRow来代替分散的功能
	export default class TodosList2 extends Component {
	    constructor(props) {
	        super(props);
	        this.state = {todos: []};
	    }
	    componentDidMount() {
	        axios.get('/todos/')
	            .then(response => {
	                this.setState({ todos: response.data });
	            })
	            .catch(function (error){
	                console.log(error);
	            })
	    }
	    //
	    todoList() {
	        return this.state.todos.map((currentTodo, i) => {
	            return <TodoRow obj={currentTodo} key={i} />;
	        })
	    }
	    //
	    render() {
	        return (
	            <div>
	                <h3>Todos List</h3>
	                <table className="table table-striped" style={{ marginTop: 20 }} >
	                    <thead>
	                        <tr>
	                            <th>Description</th>
	                            <th>Responsible</th>
	                            <th>Priority</th>
	                            <th>Action</th>
	                        </tr>
	                    </thead>
	                    <tbody>
	                        { this.todoList() }
	                    </tbody>
	                </table>
	            </div>
	        )
	    }
	}

Also, we need to create a new component called todoRow.component.js to represent each row displayed in the todo list table as below:
	
	import React, { Component } from 'react';
	import { Link } from 'react-router-dom';
	import axios from 'axios';
	// import Button from 'react-bootstrap/Button';
	// Referenced from https://www.positronx.io/react-js/
	//
	export default class TodoRow extends Component {
	    //
	    constructor(props){
	        super(props);
	        this.deleteTodo = this.deleteTodo.bind(this);
	    }
	    //
	    deleteTodo(){
	        console.log(this.props.obj._id);
	        axios.delete('/todos/delete/'+this.props.obj._id)
	            .then((res) => {
	                console.log('Todo is successfully deleted!')
	            }).catch(err => console.log(err));
	        //
	        window.location.reload();
	        return false;
	    }
	    //
	    render() {
	        return (
	            <tr>
	                <td>{this.props.obj.todo_description}</td>
	                <td>{this.props.obj.todo_responsible}</td>
	                <td>{this.props.obj.todo_priority}</td>
	                
	                <td>
	                    <Link className="edit-link" to={"/edit/" + this.props.obj._id}>
	                        Edit
	                    </Link>
	                    &nbsp;&nbsp;&nbsp;
	                    <a href='#' onClick={this.deleteTodo} size="sm" variant="danger">Delete</a>
	                </td>
	            </tr>
	        )
	    }
	}

	
## More in the future
1. Refract the code, this is a tough but interesting job. You can start your own journey.
	* We can use proxy to set axios backend server url instead of writing it in the index.js file. Set <code>"proxy": "http://localhost:3002",</code> in the frontend package.json file just below the "scripts". After you update package.json file, you must restart the frontend server with <code>npm run dev</code>.
	* Config MongoDB Atlas online free version instead of using local mongodb to store data in the backend .env file.
2. [Add AuthN and AuthZ - by passport library](https://blog.bitsrc.io/build-a-login-auth-app-with-mern-stack-part-1-c405048e3669)
3. [datapicker - Add more field](https://medium.com/@beaucarnes/learn-the-mern-stack-by-building-an-exercise-tracker-mern-tutorial-59c13c1237a1)