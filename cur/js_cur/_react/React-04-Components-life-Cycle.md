# React 04: Components life cycle

---

<details>
    <summary>🎬 Video: React -- lifecycle methods</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/-YVLy9UE5QE?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

Each class based component has several "lifecycle methods" that you can override to run code at particular times in the process.

Methods prefixed with *will* are called right before something happens, and methods prefixed with *did* are called right after something happens.

Let's have a look at some of the most common "lifecycle methods"


## componentDidMount()

`componentDidMount` is invoked immediately after a component is mounted. Initialization that requires DOM nodes should go here. If you need to load data from a remote endpoint, this is a good place to instantiate the network request. Setting state in this method will trigger a re-rendering.

```javascript
import React from 'react' 

class Example extends React.Component { 
  componentDidMount(){ 
//make an async call with axios to the dataBase to retrieve/render data after the component is mounted
  }
}
```

In this example we set state from the `componentDidMount`. We use `setTimeout` simply to have a delay to notice 'Jason' before it will be replaced by 'Robert':

```javascript
import React from 'react'; 

class App extends React.Component {
  state = { name:'Jason'}

  componentDidMount(){
    console.log('coming from componentDidMount')
    let that = this
    setTimeout(function(){ that.setState({name:'Robert'})}, 3000);
  }

  render() {
    console.log('coming from the render function')
    return (
      <div>
      <h1>{this.state.name}</h1>
      </div>
      );
  }
}
export default App;
```

<iframe src="https://codesandbox.io/embed/white-river-xnpxu?fontsize=14" title="React Block 4 - 1" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

## static getDerivedStateFromProps()

This lifecycle method is called before the component is mounted. 
It enables a component to update its internal state as the result of changes in props.

```javascript
class Parent extends React.Component {
  render(){
    return (
      <div className="App">
         <Child name={'Mario'} lastname={'Rossi'}/>
      </div>
    )
  }
}
export default Parent;
 

class Child extends React.Component{
	state = {phone:123456789}

	static getDerivedStateFromProps(props,state){
          console.log(state)
          return {name:props.name,lastname:props.lastname}
    }
	render(){
		return <h1>{this.state.name + ' ' + this.state.lastname}</h1>
		
	}
}
export default Child
```
As you can see in the example we have a Child component rendered by App.js

The `static getDerivedStateFromProps()` takes two arguments : props and state and it must return an object that modify 
the state (the equivalent of setState) or null.

props refers to the props coming from the parent component.

state give you access to the internal state before the update.

<iframe src="https://codesandbox.io/embed/ecstatic-allen-s2e7z?fontsize=14" title="React Block 4 - 2" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

## componentWillUnmount()

`componentWillUnmount()` is invoked immediately before a component is unmounted and destroyed. Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any DOM elements that were created in `componentDidMount`

When it is called? This is invoked just before the component is unmounted from the DOM. What can we do in this method? Anything you want to do before component will be removed from the render.

In this snippet we will unmount child component by clicking on the second h2 and we will see 'Noooooo!!!' in the console of DevTools coming form the `componentWillUnmount`:

```javascript
//parent
import React from 'react' 
import Child from './ChildComp.js'

class Parent extends React.Component {

  state = {user: 'Rob'} 

handleClick = (user) => {
  this.setState({user})
}

  render() {

    return (
      <div>
      <h1 onClick={()=>this.handleClick('Johanna')}>Click me {this.state.user}</h1>
      <h1 onClick={()=>this.handleClick('David')}>Click me to unmount child component</h1>
      {this.state.user !== 'David' ? <Child user={this.state.user} /> : null}
      </div>
      )
  }
}

export default Parent

// child
import React from 'react' 

class UserInfoComponent extends React.Component {

    state = {user: this.props.user} 

    static getDerivedStateFromProps(props){
       return { user : props.user}
    }

    componentWillUnmount (){
        console.log('Nooooooo!!!')
    }

    render() {
        if(this.state.user)
            return (
                <h1>{this.state.user}</h1>
                );

        return (
            <h1>loading</h1>
            )
    }
}

export default UserInfoComponent
```

<iframe src="https://codesandbox.io/embed/mystifying-sea-jmhmz?fontsize=14" title="React Block 4 -3" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

