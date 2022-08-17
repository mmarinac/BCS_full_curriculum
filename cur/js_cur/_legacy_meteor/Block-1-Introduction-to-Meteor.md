# Block 1 Introduction to Meteor
Meteor is a full-stack JavaScript platform for developing modern web and mobile applications. Meteor includes a key set of technologies for building connected-client reactive applications, a build tool, and a curated set of packages from the Node.js and general JavaScript community.
Meteor uses a proprietary protocol called DDP (Distributed Data Protocol).
DDP is a standard way to solve the biggest problem facing client-side JavaScript developers: querying a server-side database, sending the results down to the client, and then pushing changes to the client whenever anything changes in the database.

----------
[Videolesson](https://youtu.be/ZZxSsFuKMqs)

----------

Let’s start by installing Meteor on our computer!

# Windows:
****
[Download the official Meteor installer here](https://install.meteor.com/windows).

----------
# OS X ||  Linux

Run this from your terminal:

curl https://install.meteor.com/ | sh

----------

On either operating system once done installing we can get started by creating our first Meteor application, let’s cd the location on our computer where we want our application to be and let’s create it by running the following command in our terminal.


    meteor create THE_NAME_OF_YOUR_APP_GOES_HERE


----------

This may take one minute or so, after it’s done you can cd your app and then run it by simply typing the following command in your command line.


    meteor

This will start your application and will also tell you in which port your server is running!

----------

If you open your browser and go in the indicated port you will see the demo app that meteor creates as default.
You  may play a bit with it if you feel like it, or we can just get rid of it completely so that we can start fresh.

----------
# Meteor + React

We are not using the Meteor’s default engine (Blaze) here, instead we use React which works very well with Meteor.
First thing first we need to install React and ReactDom by running the following commands in your terminal.

    meteor npm install react react-dom --save


----------

In order to use React we need to go to the `client` folder in our Meteor application, get rid of everything from main.html and main.js.

In main.html replace what’s inside with the following:

    <head>
    </head>
    <body>
    <div id="app"></div>
    </body>


----------

And in main.js replace what’s inside with the following:


    import { Meteor } from 'meteor/meteor';
    //import Meteor library
    import React from 'react';
    //import React library
    import { render } from 'react-dom';
    //import the render function from react-dom
    import HelloMeteor from '../imports/HelloMeteor.jsx';
    
    //import the React component that we haven't created yet! ...oops
    
    Meteor.startup(() => {
      render(<HelloMeteor />, document.getElementById('app'));
    });
    

Now everything is fine apart from the fact that we have imported the component “HelloMeteor” which we are yet to create!

Now let’s get out of the client folder and let’s go to the root folder, once there we need to create a folder called `/imports`  please note that this is not an arbitrary name, the  `/imports`  folder has a specific meaning for Meteor.

Unlike the `/client` and `/server` directories where all code is loaded automatically following a [specific load order](http://guide.meteor.com/structure.html#load-order), any code within the project's `/imports` directory *is not* loaded automatically. This means that anything placed in this directory must be loaded explicitly in the application. Otherwise, our application won't see it.

inside our /`imports` directory/folder we can create our first React component as shown below.


    import React from 'react'
    //this imports the React library
    
    export default class HelloMeteor extends React.Component{
    //this declares the class HelloMeteor and at the same time it exports it
            render(){
            //this is the render function inside of which 
            //we have what that needs to be displayed from this component
                    return(
                    <div>
                            <h1>Hello from your first meteor app! </h1>
                    </div>
                    )
            }
    }
# TODO APP
****
Now to get familiar with Mongo and Meteor we can write the most basic example of a CRUD application a todo app.

----------
https://www.youtube.com/watch?v=ZmUvZCDZHEo&


[https://youtu.be/ZmUvZCDZHEo](https://youtu.be/ZmUvZCDZHEo)

----------

This will consist of the following

    /imports
          TodoComp.js
          TodoList.js
          TodoItem.js


    /imports/api
          todo.js


    /server
          main.js


    /client
          main.css
          main.html
          main.js


# /imports
## TodoComp.js
    import React    from 'react'
    import {Todos}  from  './api/todo'
    import TodoList from  './TodoList'
    export default class TodoComp extends React.Component{
            constructor(){
                    super()
                    this.state = {
                            todo:'',
                            todos:''
                    }
            }
    
            componentWillMount(){
                    Tracker.autorun(()=>{
                    
                            var todos = Todos.find({}).fetch()
                            debugger
                            this.setState({todos})
                    })
            }
            getTodos(e){
                    this.setState({todo:e.target.value})
            }
    
            setTodo(){
                    Todos.insert({todo:this.state.todo},(err,done)=>{
                            this.refs.input.value = ""
                    })
            }
    
            removeTodo(id){
                    Todos.remove({_id:id})
            }
            render(){
                    return(
                    <div className="wrapper">
                            <div>
                                    <input 
                                            ref = 'input'
                                            onChange = {this.getTodos.bind(this)}
                                            placeholder="add todo"/>
                                    <button 
                                            onClick={this.setTodo.bind(this)}>
                                            add todo
                                    </button>        
                            </div>
                            <div>
                                    <TodoList 
                                            todos       = {this.state.todos}
                                            removeTodo  = {this.removeTodo}
                                    />
                            </div>
                    </div>
                    )
            }
    }


## TodoList.js
****    import React                 from 'react'
    import TodoItem         from './TodoItem'
    
    export default class TodoList extends React.Component{
    
            render(){
                    return <div>
                    {
                            this.props.todos.map((ele, i)=>{
                                    return <TodoItem 
                                            todo                 = {ele.todo}
                                            key                  = {i}
                                            id                   = {ele._id}
                                            removeTodo           = {this.props.removeTodo}
                                            /> 
                            })
                    }
                    </div>
                    
            }
    }


## TodoItem.js
****    import React from 'react'
    
    export default class TodoItem extends React.Component{
            getId(id){
                    this.props.removeTodo(id)
            }
            render(){
                    return(
                            <div>
                                    {this.props.todo}
                                    <span 
                              onClick = {this.getId.bind(this, this.props.id)} >
                                            &nbsp;&nbsp; ⌫
                                    </span>
                            </div>
                    )
            }
    }

Declare a mongo collection so that we can get our todos to be persistent


    /imports/api/yourCollectionfile.js


    import {Mongo} from 'meteor/mongo'
    export const Todos =  new Mongo.Collection('todos')

In order for our collection to be permanently saved we need to also import our collection in our server  otherwise the data won’t be really saved.

    server/main.js


    import { Meteor } from 'meteor/meteor';
    import { Todos  } from '../imports/api/todo'
    
    Meteor.startup(() => {
      // code to run on server at startup
    });




# /client
## main.css
    /* CSS declarations go here */
    
    body{
            margin:0;
    
    }
    .wrapper{
            width:50%;
            display: grid;
            margin: 0 auto;
    
    }
    
    input {
            width:80%;
            grid-column:start;
            padding: 10px;
            display: inline-flex;
            border-radius: 5px;
            outline:none;
    }
    
    button{
            padding: 10px;
            display: inline-flex;
            border-radius: 5px;
            grid-column:end;
            background:black;
            color:white;
            opacity: 0.7;
            filter: alpha(opacity=50);
    }


## main.html
    <head>
    </head>
    <body>
    <div id="app"></div>
    </body>


## main.js
    import { Meteor }  from 'meteor/meteor';
    import   React     from 'react';
    import { render }  from 'react-dom';
    import TodoComp    from '../imports/TodoComp.js';
    
    Meteor.startup(() => {
      render(<TodoComp />, document.getElementById('app'));
    });



# Security in Meteor

Now our application is fine, it works in the sense of being able to add and delete our todos, however from a security prospective is a disaster as all the operations are allowed from the client side, meaning that anyone who knows how to code can easily hack our site.

As default Meteor as a package called insecure, which is as bad as it sounds!!
so now that we played a little with this let’s get rid of this package immediately.


    meteor remove insecure

As soon as you do this you will see that neither insert or delete works anymore, that’s because Meteor is no longer allowing client side operations (apart from find()).
but we can fix this right away using server side code…


# Meteor Methods

in our   `/server` folder let’s now create another folder called Methods, inside of which we can add our methods in a file named TodosMethods.js (or anything else you like…)


## TodosMethods.js
    import { Todos}   from '../../imports/api/todo'
    import { Meteor }  from 'meteor/meteor';
    
    Meteor.methods({
            addTodo:function(todo){
                    console.log("addTodo meteor method called from the server", todo)
                    Todos.insert({todo},(err,done)=>{
                            console.log(err,done)
                    })
            },
            removeTodo:function(todo){
                    console.log("remove Todo meteor method called from the server", todo)
                    Todos.remove({_id:todo})
            }
    })

and in our clients let’s replace our client-side insert and remove functions with `Meteor.call` inside your `TodoComp.jsx`

**Insert todo**

            setTodo(){
                if(this.state.todo){
                //first we check that we have a todo to submit/insert
                   Meteor.call('addTodo',this.state.todo,()=>{
                   // here we call the method 'addTodo' passing our todo and a callback
                        this.refs.input.value = ""
                        this.setState({todo:''})
                  // then inside the callback we clear our input and our state.
                   })
                }
            }

**removeTodo**

            removeTodo(id){
                    Meteor.call('removeTodo',id)
                    //call the meteor method 'removeTodo' 
                    //passing the id to remove as an argument
            }

Now our app is a bit more secure as client side insert and remove operations are no longer allowed.

However in order for our app to be a full CRUD (create read update delete) we need to add an update function, let’s do that now.


    /imports/TodoItem.jsx


            updateTodo(id, todo){
                    debugger
                    Meteor.call('updateTodo', id, todo, (err,done)=>{
                            console.log(err,done)
                    })
            }

we of course need to pass this function as prop to our child component, but I will let you figure that part out.

then our method in the server

    /server/methods/TodosMethods


    updateTodo:function(id,todo){
          console.log("update Todo meteor method the id is", id," and the todo is ", todo)
          Todos.update({_id:id},{ $set:{ todo:todo }
          })
    }


## **EXERCISE**

Our amazing todo app is almost done however there are a few tweaks you can make.


- Add the function update and the method where they need to be.
- Pass the update function to our child component through props then call it from there.
- Add an  hidden input field that can be shown on click to update the selected todo.
- Also hide the delete and edit icons  so that these are shown on mouse enter and hidden on mouse out
- Hovering on the icon update it should make it red
- Hovering on the icon delete it should make it blue
- Adding, removing and updating functions should be done through  meteor methods.

