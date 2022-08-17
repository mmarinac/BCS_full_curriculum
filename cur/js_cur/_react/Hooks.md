# React Hooks

----------

React Hooks is a feature first implemented in version 16.7 that allows us to use react class components features in function components, like state, lifecycle or context.

## useState

---

<details>
    <summary>🎬 Video: React -- useState</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/Q2y9Z3pd81o?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

[Sample code from the video lesson](https://gitlab.com/snippets/1969133)

---

With useState we can add and modify a local state in a function component.

```javascript
import React, { useState } from 'react';

const App = () => {
  const [count, setCount] = useState(0);
}
```
First we import useState from the react package, then we declare a variable which contains the name of the key in the state and the name of the method that we are going to use to modify it.

The value that we are passing to useState (in this case 0), is the initial value of count


```javascript
import React, { useState } from 'react';

const App = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      {console.log(count)}
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
In the example when we click the button we call the setCount method that increase our count value by one.

To retrieve the count's value we just type count instead of this.state.count

<iframe src="https://codesandbox.io/embed/friendly-chatelet-nq7z2?fontsize=14" title="React Hooks 1" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

We can declare as many state variables as we need

```javascript
import React, { useState } from 'react';

const App = () => {
  const [count, setCount] = useState(10);
  const [users, setUsers] = useState([{user:'Mario',_id:'1'},{user:'Luisa',_id:'2'},{user:'Francesca',_id:'3'}])
  const [fruit, setFruit] = useState('banana')
}
```

Now let's see a form example using hook's

```javascript
import React, { useState } from 'react';

const App = () => {

  const [email, setEmail] = useState('');
  const [pass,  setPass ] = useState('');

  const handleNameChange = (e) => setEmail(e.target.value)
  const handlePassChange = (e) => setPass(e.target.value)

  return (
    <div className='main'>
       <form onSubmit={event => {
                event.preventDefault();
                console.log(email,pass);
             }}>

          <div className='child'>email
              <input onChange={handleNameChange}/>
              <p>{email}</p>
          </div>

          <div className='child'>password
              <input onChange={handlePassChange}/>
              <p>{pass}</p>
          </div>
          <button>SUBMIT</button>
       </form>
    </div>
  );
}

export default  App
```

<iframe src="https://codesandbox.io/embed/flamboyant-ritchie-xr6c2?fontsize=14" title="React Hooks  2" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>


## useEffect

---

<details>
    <summary>🎬 Video: React -- useEffect</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/L7me9ZY8vBc?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

This hook is called after the component has been mounted, it works like componentDidMount or componentDidUpdate in class based components, in fact this method
is called after the first render and after every re-render.

We also need to import useEffect from the react package

```javascript
import React, { useState, useEffect } from 'react';

const App = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log('after rendering')
  });

  return (
    <div>
      {console.log('from the render')}
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

export default App
```

<iframe src="https://codesandbox.io/embed/awesome-star-og1o2?fontsize=14" title="React Hooks 3" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

As you can see in the example it takes one argument, a function, where we have the code to be executed when the method is called.

In case that we want the method to be called only on the first render, we can pass a second argument, an empty array, if you want to keep track of some specific variables from state then you provide an array with names of these variables.

```javascript
import React, { useState, useEffect } from 'react';

function App() {
  const [count, setCount] = useState(0);

  const getCount = () => {
      console.log(count);
  }

  useEffect( () => {
    getCount();
  }, []);

  return (
    <div>
      <button onClick={()=>setCount(count=>count+1)}>count</button>
      {count}
    </div>
  );
}

export default App;
```

<iframe src="https://codesandbox.io/embed/quizzical-gould-52fl9?fontsize=14" title="React Hooks 4" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

As you can see we receive only the first console.log from the getCount function. 

### Lifecycles --> uesEffect replacements cheat sheet


#### componentDidMount

```javascript
// with ccomponentDidMount()
componentDidMount() {
    console.log('Triggering once');
}

// with useEffect()
useEffect(() => {
    console.log('Triggering once');
}, [])
```

#### componentDidUpdate

```javascript
// with ccomponentDidUpdate()
componentDidUpdate(prevProps) {
    console.log(`Triggering after ${prevProps} was updated`);
}

// with useEffect()
useEffect(() => {
    console.log('Triggering after "prevProps" was updated; can watch any state variable(s) passed inside array');
}, [prevProps])
```

#### componentWillUnmount

```javascript
// with ccomponentDidUnmount()
componentWillUnmount() {
    console.log('Goodbye, I am unmounting');
}

// with useEffect()
useEffect(() => {
    console.log('Goodbye, I am unmounting');
    return () => {
        console.log('Do some cleanup');
    }
}, [])
```
  

## useRef

With [useRef](https://reactjs.org/docs/hooks-reference.html#useref) we can access our DOM elements by "ref" which we assign or in other words by a "nickname" which we can use later to manipulate a specific element. It could be useful in case then element which triggered an event is not related to the target element, for example:

<iframe src="https://codesandbox.io/embed/useref-cth14?autoresize=1&fontsize=14&hidenavigation=1&module=%2Fsrc%2FApp.js&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="useRef"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

## useContext

---

<details>
    <summary>🎬 Video: React -- useContext, useStateWithCallback</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/y2q6nTKfKMc?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

Another useful hook is useContext, that allows us to use the react context in function components.
With context we can pass data through the children components without the needing to pass down props manually.

### Lets see an example with classes

```javascript
//==================== context.js =========================

import React from 'react'
export const SomeContext = React.createContext()

//====================== App.js ===========================

import React from 'react'
import  FirstChild     from './FirstChild'
import { SomeContext } from './context'

export default class App extends React.Component {
  render() {
  	console.log(SomeContext.provider)
    return (
      <SomeContext.Provider value='red'>
         <FirstChild/>
      </SomeContext.Provider>
    );
  }
}

//==================== FirstChild.js =======================

import React, { Component } from 'react'
import SecondChild from './SecondChild' 
// A component in the middle doesn't have to
// pass the props down explicitly anymore.
export default class FirstChild extends Component {
  render(){
      return (
	    <div>
	      <SecondChild/>
	    </div>
	  );
  }
}

//==================== SecondChild.js ======================

import React from 'react'
import { SomeContext } from './context'

export default class SecondChild extends React.Component {

  static contextType = SomeContext;
  render() {
  	console.log(this.context)
    return <SomeContext.Consumer>
               {value => <h1 style={{color:value}}>{value}</h1>}
           </SomeContext.Consumer>
  }
}
```

<iframe src="https://codesandbox.io/embed/broken-smoke-i2yp3?fontsize=14" title="React Hooks 5" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

In the context file we create a new context and we export it for later import in the component where we need it.

The new context gives us access to two components, a Provider and a Consumer.

- The Provider is used to define the data you want to store (App.js)
- We use the Consumer where ever we need the data from the store (SecondChild.js)
 

### Now the same example with the useContext Hook

```javascript
//==================== context.js =========================

import React from 'react'
export const SomeContext = React.createContext()

//====================== App.js ===========================

import React from 'react'
import  FirstChild     from './FirstChild'
import { SomeContext } from './context'

const App = () => <SomeContext.Provider value='orange'>
                      <FirstChild/>
                  </SomeContext.Provider>

export default App

//==================== FirstChild.js =======================

import React, { Component } from 'react'
import SecondChild from './SecondChild' 

const FirstChild = () => <SecondChild/>

export default FirstChild

//==================== SecondChild.js ======================

import React, { useContext } from 'react'
import { SomeContext } from './context'

const SecondChild = () => {
  const value = useContext(SomeContext);
  return <h1 style={{color:value}}>{value}</h1>
}

export default SecondChild
```

<iframe src="https://codesandbox.io/embed/musing-meninsky-sc0wn?fontsize=14" title="React Hooks 6" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

And here is a sandbox for passing data between sibling components:

<iframe
     src="https://codesandbox.io/embed/context-with-4-nodes-u78ou?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="context with 4 nodes"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

## useStateWithCallback

With this hook we can easily assign a function to be executed every time **after** there was some update in state and we do not need to use useEffect for this:

```javascript
import React from 'react';
import useStateWithCallback from "use-state-with-callback";

const App = () => {

  const [count, setCount] = useStateWithCallback(0, count => {
    console.log(count);
  })

  return (
    <div>
    <p>{count}</p>
    <button type="button" onClick={() => setCount(count + 1)}>
    Increase
    </button>
    </div>
    );
  };

export default App;
```

<iframe
     src="https://codesandbox.io/embed/usestatewithcallback-1rsvr?expandDevTools=1&fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="useStateWithCallback"
     allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media; usb"
     sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"
   ></iframe>




   ## react-use – a huge collection of custom hooks:

   https://github.com/streamich/react-use