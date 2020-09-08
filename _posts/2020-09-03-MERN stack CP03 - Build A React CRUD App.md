---
layout:     post
title:      2020-09-03-MERN stack CP03 - Build A React CRUD App
subtitle:   Bridge Frontend to Backend
date:       2020-09-03
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
<strong>Note</strong>:In Markdown, you can use empty row + tab space to make a code block. Markdown would auto wrap tab leading lines within &lt;pre&gt;&lt;code&gt;.<br/>

In the third part, we are going to build the bridge between the frontend to backend.

## [Axios - The library to bridge](https://www.npmjs.com/package/axios)
<strong>Note</strong>: [Diff between Axios and Fetch API](https://blog.logrocket.com/axios-or-fetch-api/)
In order to be able to send HTTP request to backend, we need to install Axios library with <code>$ npm install axios</code>

### Update create_todo.component.js file as below:

	//add import statement
	import axios from 'axios';
	//update onSubmit() function
	onSubmit(e) {
		e.preventDefault();
		//
		console.log(`Form submitted:`);
		console.log(`Todo Description: ${this.state.todo_description}`);
		console.log(`Todo Responsible: ${this.state.todo_responsible}`);
		console.log(`Todo Priority: ${this.state.todo_priority}`);
		//
		const newTodo = {
			todo_description: this.state.todo_description;
			todo_responsible: this.state.todo_responsible;
			todo_priority: this.state.todo_priority;
			todo_completed: this.state.todo_completed;
		};
		//
		axios.post('http://localhost:3002/todos/add', newTodo)
			.then(res => console.log(res.data));
		//
		this.setState({
			todo_description: '',
            todo_responsible: '',
            todo_priority: '',
            todo_completed: false
			})
	}


### Update todos_list.component.js file as below

	import { Link } from 'react-router-dom';
	import axios from 'axios';
	//
	const Todo = props => {
		<tr>
			<td>{props.todo.todo_description}</td>
			<td>{props.todo.todo_responsible}</td>
			<td>{props.todo.todo_priority}</td>
			<td>
				<Link to={"/edit/"+props.todo._id}>Edit</Link>
			</td>
		</tr>
	}
	//
	export default class TodosList extends Component {
		constructor(props){
			super(props);
			this.state = {todos: []};
		}
		//retrieve the todos data from database
		componentDidMount(){
			axios.get('/todos/')
				.then(response => {
					this.setState({todos: response.data});
				})
				.catch(err => console.log(err));
		}
		//
		render(){
			return (
				<div>
					<h3>Todos List</h3>
					<table className = "table table-striped" style={{
						marginTop:20}}>
						<thead>
							<tr>
								<th>Description</th>
								<th>Responsible</th>
								<th>Priority</th>
								<th>Action</th>
							</tr>
						</thead>
						<tbody>
							{ this.todoList()}
						</tbody>
					</table>
				</div>
			)
		}
		//Output a row of table each time by map function
		todoList(){
			return this.state.todos.map((currentTodo, i) => {
					return <Todo todo={currentTodo} key={i} />;
				})
		}
	}
