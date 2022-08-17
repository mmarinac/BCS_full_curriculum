# State

---

<details>
    <summary>🎬 Video: React -- state, events, passing data from child to parent</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/IlhlmMhAtTk?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

Sample code from the video lesson:

<iframe src="https://codesandbox.io/embed/wonderful-sid-v4gq6?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="wonderful-sid-v4gq6"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

---

The heart of every React component is its “state”, an **object** that determines how that component renders & behaves. In other words, “state” is what allows you to create components that are dynamic and interactive.

State allows you to dynamically change many elements at once based on one variable. State encompasses the key parts of your UI that changes based on user input.

With less things to keep track of in state, you will be able to write components with more clarity and fewer opportunities for bugs. 

When state changes, many components may change in accordance based on the one variable.

**STATE EXAMPLE**

![](https://barcelonacodeschool.com/files/pics/event-handler-state-rerender.png)

```javascript
import React from 'react';
//require React 

class Statefull extends React.Component{ 

  state = {
    name:'Luke',
    lastname: 'Skywalker'
  } 
  // state is nothing but an object

  render(){ 
    return <h1>Hi, my name is {this.state.name} {this.state.lastname}</h1> 
  }}

export default Statefull; //Export your component
```

This will render an H1 displaying the values from our state object.

In order to change the state we need to use the `setState` function.

The main thing to note about this.setState is that **it is what we use to we make our component re-render.** Everytime you change state, the component will re-render. 

Another thing to keep in mind using state is that you cannot modify the state directly :

```javascript
this.state.name = 'Adriana' // wrong , it wont re-render the component
```
```javascript
this.setState({name:'Adriana'}) // correct
```
To update an existing value in the state we need first to get it from the state, assign to a variable, modify it and then replace in the state:
```javascript
let { counter } = { ...this.state };
    counter += 1;
    this.setState({ counter });
```

> `{ ...this.state }` will make a copy of object literal here instead if just referring to the state object 

# Handling Events with JSX

## onClick

The `onclick` event from pure JavaScript lets us call a particular piece of code when the user clicks or taps a particular item. You can use this in React too, but the syntax is a little different -- it is `onClick`. 

```javascript
import React from 'react'

class App extends React.Component {

  buttonClicked = ()=> {
    console.log('Button was clicked!')
    // this will happen every time you click the button
  }

  render() {
    return <div>
               <button onClick={this.buttonClicked}>Click me</button>
               {/* this button calls buttonClicked function once it is clicked */}
           </div>
  }
}
export default App
```

<iframe src="https://codesandbox.io/embed/react-block-3-1-forked-ixnmu?fontsize=14" title="React Block 3 -1" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

Of course this is not too useful, but we can use the onClick event for instance to display an alert popup with some value from the state:

```javascript
import React from 'react'

class App extends React.Component{

  state = {
    name:'Luke',
    lastname: 'Skywalker'
  } 

  getDataOnClick = () =>{

    alert(`Hello ${this.state.name} ${this.state.lastname}`)
  }

  render(){

    return <div>
              <button onClick = {this.getDataOnClick}>click me</button>        
           </div>
  }
}
export default App
```

<iframe src="https://codesandbox.io/embed/react-block-3-2-forked-55qgz?fontsize=14" title="React Block 3 - 2" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

> 👉 [Sandbox with example to render elements in the loop and track click on each one with index](https://codesandbox.io/s/render-elements-in-the-loop-and-track-click-on-each-one-with-index-46zg0) 👈 

## onChange

The onChange event allows us to get the data as soon as it’s written in our input field (or elsewhere) without the need to click the button.

```javascript
import React from 'react'

class App extends React.Component{

  handleChange = e =>{
    var data = e.target.value
    console.log(data)
  }

  render(){
    return <div> 
            <input onChange={this.handleChange}/> 
           </div>
  }
}
export default App
```

<iframe src="https://codesandbox.io/embed/nifty-nightingale-xlqjb?fontsize=14" title="React Block 3 - 3" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

## onSubmit

The onSubmit event can only be triggered from within a from, either by pressing the enter key on the keyboard or by pressing the submit button (if there is one), here is an example without it.

```javascript
import React from 'react'

class App extends React.Component{
  handleSubmit =(e)=>{
    //e.preventDefault()
    //the preventDefault method is needed to prevent reloading the page which is default behavior for submitting the forms

    var data = e.target.firstElementChild.value
    alert(data)
  }

  render(){
    return <form onSubmit={this.handleSubmit}> 
              {/* our form only have one input field and we can submit it buy pressing Enter key on the keyboard */}
              <input/>
          </form>
  }
}
export default App
```

<iframe src="https://codesandbox.io/embed/react-block-3-4-i6pm9?fontsize=14" title="React Block 3 - 4" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

We can of course mix these events together, let’s for example use the `onChange` event to get the data from the input and the `onSubmit` to `alert` it on submit.


```javascript
import React from 'react'

class App extends React.Component {
  state = {
    userInput: ""
  };

  handleSubmit = (e) => {
    // prevent page from reloading onSubmit which is default behavior
    e.preventDefault();
    // alert the data from state
    alert(this.state.userInput);
  };

  handleChange = (e) => {
    // data is a string form the input
    let data = e.target.value;
    // setting the content of input to be the value of 'userInput' in state
    this.setState({ userInput: data });
  };

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input onChange={this.handleChange} />
        <button>Done!</button>
      </form>
    );
  }
}
export default App;
```

<iframe src="https://codesandbox.io/embed/crazy-oskar-lk0lo?fontsize=14" title="ReactB3onChange_onSubmit_manipulating_data_while_onChange" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media; usb" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>


## Controlled components

In React we can still get data from the input and control what’s displayed in the input even without using refs, we can do that using what’s known as a controlled component.

In a controlled component the value of the input itself comes from the state and viceversa.

```javascript
import React from 'react';

class App extends React.Component {

  state = { text:'', shown:'' }
  // in state we define initial empty values

  handleChange = e =>{
    this.setState({[e.target.name]:e.target.value})
    // here we update state for every character entered by user
  }

  handleShow = ()=> {
    this.setState({shown:this.state.text},()=>{
      // here we clone value from 'text' to 'shown' in the state object
      this.setState({text:''})
      // and clear the 'text' value in the state which also clears the input on the page
    })
  }
  render() {
    return <div>
               <input 
                   onChange = {this.handleChange}
                   name = "text" 
                   value = {this.state.text}/>
      {/* the value or visible text in this input is coming from the state itself */}
               <h1>{this.state.shown}</h1>
      {/* this h1 as also coming form the state */}
               <button onClick={this.handleShow}>show text</button>
           </div>
  }
}
export default App
```

<iframe src="https://codesandbox.io/embed/dreamy-glade-uw44l?fontsize=14" title="React Block 3 - 5" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

## Getting data from a Child component with a function 

As props are always passed form the parent component to the child, to send data in reverse, from child into the parent, we can use a function.

We simply pass the function to the child and then from the child we call the function passing whatever data we need to pass to the parent.

```javascript
// your parent component, ie App.js
import Child from './Child'
import React from 'react'

class App extends React.Component {

  getData  = data => console.log(`Child component sends ${data}`)

  render(){
    return <div>
              <Child getData = {this.getData} />
           </div>
  }
}
export default App
```

```javascript
//your child component, ie Child.js
import React from 'react'

class Child extends React.Component {
  render(){
  return <button onClick ={()=>this.props.getData('banana')}>send banana to the parent</button>
    {/*onClick we execute this function and passing some arguments 'banana' to be delivered to the parent*/}
  }
}
export default Child
```
<iframe src="https://codesandbox.io/embed/admiring-mccarthy-ry3le?fontsize=14" title="React Block 3 - 6" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

## Example Snippets

```javascript
//onChange Event
import React, { Component } from 'react';

class App extends Component {
  state = {
    email:'', password:'', username:''
  }

  handleChange = event => {
    let name = event.target.name;
    let value = event.target.value;
    //let { name, value } = event.target;
    this.setState({[name]:value});
   }
  
  render() {
    return(
            <div onChange = {this.handleChange}>
              <input 
              name= 'email'
              value ={this.state.email} 
              />
              <input 
              name= 'username'
              value ={this.state.username} 
              />
              <input 
              name= 'password'
              value ={this.state.password} 
              />
              
              <h1>{this.state.email}</h1>
              <h1>{this.state.username}</h1>
              <h1>{this.state.password}</h1>
           </div>
      );
  }
}

export default App;
```

<iframe src="https://codesandbox.io/embed/delicate-sky-o3vy2?fontsize=14" title="React Block 3 - 7" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

```javascript
// onChange, onMouseLeave, onMouseEnter, onSubmit, onClick events
import React, { Component } from 'react';

class App extends Component {
  state = {
    email:'', password:'', username:''
  }

  handleChange = event => {
    let name = event.target.name;
    let value = event.target.value;
     //let { name, value } = event.target;
     this.setState({[name]:value});
   }

   handleSubmit = e => {
    e.preventDefault();
    const { email, password, username} = this.state;
    alert(email +' '+ password+' '+ username)
  }

  handleMouseEnter = ( ) => console.log('handleMouseEnter called')

  handleMouseLeave = () => console.log('handleMouseLeave called')

  handleClick = () => console.log('handle click fn called!');
  
  render() {
    return (
      <div>
        <form 
        onMouseLeave = {this.handleMouseLeave}
        onMouseEnter ={this.handleMouseEnter}
        onSubmit = {this.handleSubmit}>
        
          <input 
          onChange = {this.handleChange}
          name= 'email'
          value ={this.state.email} 
          />
          <input 
          onChange = {this.handleChange}
          name= 'username'
          value ={this.state.username} 
          />
          <input 
          onChange = {this.handleChange}
          name= 'password'
          value ={this.state.password} 
          />

          <button>Press me please!</button>

          <h1>{this.state.email}</h1>
          <h1>{this.state.username}</h1>
          <h1>{this.state.password}</h1>
        </form>
        <button onClick={this.handleClick}>click me too</button>
      </div>
      );
  }
}

export default App;
```

<iframe src="https://codesandbox.io/embed/serene-morning-h59ee?fontsize=14" title="React Block 3 - 8" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

## Example Zip:
<a href="../code_examples/state_events_lecture.zip" download>Click to Download</a>


# Exercise time!

One of the exercises would be a ToDo App:

## React ToDo app
----------

Create a todo app according to the following requirements:

- it needs to have a input field.
- it needs to have a submit button
- you need to be able to submit pressing the button but also pressing enter.
- you need to be able to remove todo clicking on a trashcan icon or something as obvious
- the delete icon needs to be hidden until hovering on the todo.
- you need to be able to mark todos as done with a line through or something as obvious.

You need to have this in GitLab from the very beginning and keep it up to date so that we can check your progress from your repo.

Examples: http://todoerapp.surge.sh, http://todoornottodo.surge.sh/

