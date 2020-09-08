---
layout:     post
title:      2020-09-07-MERN stack CP05 - Add Date field
subtitle:   How to add a date field in existing MERN app
date:       2020-09-07
author:     BY Elon
header-img: img/post-bg-BJJ.jpg
catalog: true
tags:
    - MERN
    - REST
    - datepicker
---
There is a possible way for us to use date field in our web page. That's JQuery UI - [Datepicker](https://jqueryui.com/datepicker/) widget. To add the widget, we need to use <code>$ npm install react-datepicker</code> to install it.

Then, we need to do below modifications in our existing MERN app:
1. In the backend, update our current model todo.model.js to include a creationDate field as well as timestamps field:
	
		todo_creationDate:{
			type: Date,
			required: true
		}
		{timestamp: true}

Also, in todo.route.js, we need to update create and update todo route to include todo_creationDate field. If not, it would cast 400 err when inserting or updating record into DB.
	
	todo.todo_creationDate = req.body.todo_creationDate;

2. In our frontend, there are multiple places to be modified.
	* In todo_list2.component.js, add CreationDate in the table head.
	* In todoRow.component.js, add this.props.obj.todo_creationDate in the render() function.
	* Update todo_list.component.js as below:

			const Todo = props => (
			    <tr>
			        <td>{props.todo.todo_description}</td>
			        <td>{props.todo.todo_responsible}</td>
			        <td>{props.todo.todo_priority}</td>
			        <td>{!(props.todo.todo_creationDate) ? "" : 
			            props.todo.todo_creationDate.substring(0, 10)}</td>
			        <td>
			            <Link to={"/edit/"+props.todo._id}>Edit</Link> | 
			            <a href="#" onClick={() => {props.deleteTodo(props.todo._id)}}>Delete</a>
			        </td>
			    </tr>
			)
			//Add a deleteTodo method and bind it when clicked
			export default class TodosList extends Component {
			    constructor(props) {
			        super(props);
			        this.state = {todos: []};
			        this.deleteTodo = this.deleteTodo.bind(this);
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
			    //Attention, here we construct return JSX code as <Todo> label which will be used as a table row in web page.
			    todoList() {
			        return this.state.todos.map((currentTodo, i) => {
			            return <Todo todo={currentTodo} deleteTodo={this.deleteTodo} key={i} />;
			        })
			    }
			    //The delete method will call axios.delete to the backend
			    deleteTodo(id){
			        axios.delete('/todos/delete/' + id)
			            .then((res) => {
			                console.log('Todo is successfully deleted!')
			            }).catch(err => console.log(err));
			        //after deletion, refresh the todos list
			        this.setState({
			            todos: this.state.todos.filter(tl => tl.id !== id)
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
			                            <th>CreationDate</th>
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
	* In edit_todo.component.js, we add two below import statements
			
			import Datepicker from 'react-datepicker';
			import "react-datepicker/dist/react-datepicker.css";
			//Add below statement in the newTodo item.
			todo_creationDate: !(this.state.todo_creationDate) ? new Date() : this.state.todo_creationDate

	* In the create_todo.component.js, we update it as below:

			this.onChangeTodoCreationDate = 
			this.onChangeTodoCreationDate.bind(this);
			//Add onChangeTodoCreationDate(date) method, different from
			//other onChange methods
			onChangeTodoCreationDate(date){
			this.setState({
				todo_creationDate: date
			});}
			//In the render() part, we add below
			<div className="form-group">
	            <label>CreationDate: </label>
	            <div>
	            <DatePicker
	                selected={this.state.todo_creationDate}
	                onChange={this.onChangeTodoCreationDate}/>
	            </div>
	        </div>

## Conclusion
After the modification, we can either test on webpage after you <code> npm run dev</code> or test it with Postman API.

### Bugs
1. Bug1: 2020-09-07, How to show date correctly
Backend automatically will convert local time to UTC time zone and store them in the database.
Solution: before sending to backend, we manually substract the incremental of UTC zones.
Like in create_todo.component.js file, we did it as below:
	
		const conv_date = new Date(this.state.todo_creationDate.getTime() -
		this.state.todo_creationDate.getTimezoneOffset()*60000);
		//
		const newTodo = {
			todo_description: this.state.todo_description,
            todo_responsible: this.state.todo_responsible,
            todo_priority: this.state.todo_priority,
            todo_completed: this.state.todo_completed,
            todo_creationDate: conv_date
		};

2. Bug2: Delete does not work well when refresh the page. Because in the todo_route.js file, delete method, I include res.redirect("/todos/") if delete the item successfully. This is incorrect. We would better not use res.redirect() here, change it to () => res.status(200).log(...)