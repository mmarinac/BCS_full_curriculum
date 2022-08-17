
# React 06: React Router 

> Official docs: https://reactrouter.com/docs/en/v6

---

<details>
    <summary>🎬 Video: React -- router</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/CtKS6KAIisw?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

[Sample code from the video lesson](https://gitlab.com/gk3000/react_router_dynamic_routes_snippet_from_curriculum)

<iframe src="https://codesandbox.io/embed/serverless-architecture-yfdkd?fontsize=14&module=%2Fsrc%2FApp.js&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="serverless-architecture-yfdkd"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

---

React router allows us to do client side routing, enabling us to render separate components without ever refreshing the page. We can create URLs and for every URL render a separate component so we will have a fully functioning navigation system with different "pages" for every URL. 

In order to use react router we need to start by installing it in the project's folder.

    npm i react-router-dom 

Then in ./src 

**App.js**

```javascript
import React from "react";
// importing Router, Route and Routes elements from the router
import { BrowserRouter as Router, Route, Routes } from "react-router-dom";
import Home from "./Home";
import About from "./About";

import "./styles.css";

export default function App() {
  return (
    <div className="App">
{/* Declaring the router which will hold al the routes/URLs*/}
      <Router>
{/* We need to use the Routes wrapper */}
        <Routes>
{/* For every URL we can render a separate component */}
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
        </Routes>
      </Router>
    </div>
  );
}
``` 

<iframe src="https://codesandbox.io/embed/react-router-1-forked-vp1dj?fontsize=14&hidenavigation=0&module=%2Fsrc%2FApp.js&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="react router 1"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

The above code allows us to render two separate components, each assigned to its own URL.

The index route “/” will render our Home component, and the “/about” route will render our About component.

Now we could manually change the URL and go from one page to the other by typing the URL in the browser's address bar, however if we were to do that it would trigger refreshing of the page each time and that’s not what we want.

---

So let’s create a navigation bar to move between the pages:

    ./src/Navbar.js

```javascript
import React from "react";
// We need to import the NavLink component from the router
import { NavLink } from "react-router-dom";

const Navbar = () => {
  return (
    <div style={styles.navStyles}>
{/* For every NavLink element we can specify the URL and the label */}
      <NavLink
        style={(isActive) => (isActive ? styles.active : styles.default)}
// This would be the URL
        to={"/"}
      >
{/* This would be the label */}
        Home
      </NavLink>

      <NavLink
        style={(isActive) => (isActive ? styles.active : styles.default)}
        to={"/about"}
      >
        About
      </NavLink>
    </div>
  );
};

export default Navbar;

const styles = {
  navStyles: {
    display: "flex",
    height: 60,
    alignItems: "center",
    justifyContent: "space-around"
  },
  active: {
    color: "red"
  },
  default: {
    textDecoration: "none",
    color: "black"
  }
};
```

Then we can define 2 pages for components:

**./src/Home.js**

```javascript
import React from "react";

const Home = () => {
  return <h3 style={styles}>HOME COMPONENT</h3>;
};

export default Home;

const styles = {
  marginTop: "20%",
  textAlign: "center"
};
```

**./src/About.js**

```javascript
import React from "react";

const About = () => {
  return <h3 style={styles}>ABOUT COMPONENT</h3>;
};

export default About;

const styles = {
  marginTop: "20%",
  textAlign: "center"
};
```

Now we can add our navbar to our router:

    ./src/App.js

```javascript
import React from "react";
import ReactDOM from "react-dom";
import { BrowserRouter as Router, Route, Routes } from "react-router-dom";
import Home from "./Home";
import About from "./About";
import Navbar from "./Navbar";

import "./styles.css";

function App() {
  return (
    <Router>
{/* Our NavBar component will be inside the Router but outside the routes */}
      <Navbar />
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Router>
  );
}

export default App
```

<iframe src="https://codesandbox.io/embed/react-router-2-forked-dlpxq?fontsize=14&hidenavigation=0&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="react router 2"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

Now the Navbar component will be available in all our routes.

---

## Dynamic routes

Now let’s open our App.js file and create our first dynamic route, it will allow us to pass some variable along when redirecting so that when we go to the next page (component) we can access this data there.

In order to tell the router that part of the route is dynamic we are going to add a **:**  right after the  **/** 
This will allow us to use variables instead of static words.

```javascript
import About from "./About.js";
import Home from "./Home.js";
import Data from "./Data.js";
import React from "react";
import ReactDOM from "react-dom";
import { BrowserRouter as Router, Route, Routes } from "react-router-dom";
import Navbar from "./Navbar";

const App = () => {
  return (
    <Router>
      <div>
        <Navbar />
        <Routes>
          <Route exact path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
{/* Now if we will trigger route /data we can pass some actual data after /data/ which is represented in the route by placeholder with the name "data" and a colon before -- :data */}
          <Route path="/data/:data" element={<Data />} />
        </Routes>
      </div>
    </Router>
  );
};

export default App
```
    
Now let’s tweak a bit our Home.js file so that we can redirect to a new component passing a string stored in a variable.

**./src/Home.js**

```javascript
import React from "react";
import { NavLink } from "react-router-dom";
var secret = "this-is-totally-a-secret";
let url = `/data/${secret}`;

const Home = () => {
  return (
    <div>
      <h1>I am HOME page</h1>
      <h2>
{/* If we will click this link below it will take us to the /data/this-is-totally-a-secret 
this-is-totally-a-secret is the actual data which we pass inside the URL itself */}
        <NavLink to={url}>Go</NavLink>
      </h2>
    </div>
  );
};

export default Home;
```

Now all we need to do to see if this works is to create the component we are trying to go to.

    ./src/Data.js

Inside it we will be able to access the variable we passed in the URL (by the name of `data`) using `useParams` hook:

```javascript
import React from "react";
// Importing useParams from the router
import { useParams } from "react-router-dom";

const Data = () => {
// declaring a variable "params" which will use useParams hook to retrieve data from the URL
  let params = useParams();

  return (
    <div>
// accessing "data" in params which will be the phrase "this-is-totally-a-secret" we are passing from the Home component
      {params.data}
      <p>
        As you can see we get our secret data send as params from the HOME page.
      </p>
    </div>
  );
};

export default Data;
```

<iframe src="https://codesandbox.io/embed/znnryp87ox?fontsize=14" title="React 06: React Router lecture" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

---

There are other ways to pass data using the router, but the good thing about using params is that the data passed this way is now part of the URL and this means it will persist on page refresh and could be bookmarked.

This would be especially useful in cases when you pass the ID of a post or a product to the single item component, as you want your link to persist when the page is refreshed.

If you need to pass props to a component from the router, you can do it directly through the Route and pass the props to the component as you normally would do to pass props from parent to child component.

In the example below we pass props to the `about` component.


```javascript
import React from "react";
import ReactDOM from "react-dom";
import { BrowserRouter as Router, Route, Routes } from "react-router-dom";
import About from "./About.js";
import Home from "./Home.js";
import Navbar from "./Navbar";

function App() {
  return (
    <Router>
      <Navbar />
      <Routes>
        <Route path="/" element={<Home />} />
{/* When user will go the the "/about" URL we will render About component and pass "mike" through the params to it */}
        <Route path="/about" element={<About username="mike" />} />
      </Routes>
    </Router>
  );
}
```

<iframe src="https://codesandbox.io/embed/react-router-4-txmv9?autoresize=1&expandDevTools=1&fontsize=14&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="react router 4"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

In the next example the route `about` is passing the function `isLoggedIn` to the component About and we can see it in `prop` printed from `About.js`:

<!-- tabs:start -->
#### **Class components**
```javascript
import React from "react";
import { BrowserRouter as Router, Route, Routes } from "react-router-dom";
import About from "./About.js";
import Home from "./Home.js";
import Navbar from "./Navbar";

export default class App extends React.Component {
  state = {
    user: {
      name: "mario",
      lastname: "rossi",
      _id: 1234,
      logged: true
    }
  };

  isLoggedIn = () => this.state.logged;

  render() {
    return (
      <Router>
        <Navbar />
        <Routes>
          <Route path="/" element={<Home />} />
          <Route
            path="/about"
            element={<About isLoggedIn={this.isLoggedIn} />}
          />
        </Routes>
      </Router>
    );
  }
}
```

#### **Function components**
```javascript
import React, { useState } from 'react';
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import About from './About.js';
import Home from './Home.js';
import Navbar from './Navbar';

export default function App() {
	const [ user ] = useState({
		name: 'mario',
		lastname: 'rossi',
		_id: 1234,
		logged: true
	});

	const isLoggedIn = () => user.logged;

	return (
		<Router>
			<Navbar />
			<Routes>
				<Route path="/" element={<Home />} />
				<Route path="/about" element={<About isLoggedIn={isLoggedIn} />} />
			</Routes>
		</Router>
	);
}
```
<!-- tabs:end -->

<iframe src="https://codesandbox.io/embed/react-router-5-pu3nc?fontsize=14&hidenavigation=0&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="react router 5"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

---

## The Navigate component

The Navigate component is used to redirect the user to the specific URL. For example, we have some app logic and based on the condition want to render either one component or another. 

In this example below once the route `/contact` will be hit we check if value of `isLoggedIn` in state is true then we render `Contacts` component. However if the value of `isLoggedIn` is false we are using `Navigate` component to redirect user to the `'/'` route which will render `Home` component. 

Remember to import Navigate component first from `react-router-dom`

```javascript
import React, {useState} from 'react';
import './App.css';
import Home from './Home'
import About from './About'
import Contacts from './Contacts'
import Navbar from './Navbar'
import Footer from './Footer'
import SingleProduct from './SingleProduct'

import {BrowserRouter as Router, Route, Routes, Navigate} from 'react-router-dom'

export default function App() {

  const [isLoggedIn]=useState(false)

  return (

    <div className='App'>
    <Router>
    <Navbar />
    <Routes>
    <Route path='/' element={<Home/>} />
    <Route path='/about' element={<About year={2020} />} />
{/* Inside the value of "element" property we have a condition checking the value of "isLoggedIn" and if it is true we render Contacts component otherwise we use Navigate to send user to "/" */}
    <Route path='/contact' element ={ !isLoggedIn ? <Navigate to='/' /> : <Contacts/> } />
    <Route path='/singleproduct/:product' element={<SingleProduct/>} />
    </Routes>
    </Router>

    <Footer />
    </div>

    )
}
```

<iframe src="https://codesandbox.io/embed/react-router-6-k5zv0?fontsize=14&hidenavigation=0&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="React Router 6"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>


Take a note on how we are using `useNavigate` and `useLocation` hooks in our `About.js` component: `useNavigate` is to send a user to another URL and `useLocation` to get the current URL:

```javascript
// we need to import useNavigate and/or useLocation hooks from react first:
import { useLocation, useNavigate } from "react-router-dom";

// then to get the current URL we can do this:
let location = useLocation();
// location will contain the current URL of the view

// to be able to send user to another URL we can activate useNavigate first:
let navigate = useNavigate();
// and then we can use it in our logic or assign to an event to send user where we want to:

  <p onClick={() => navigate(-1)}>go back</p>
// if user will click on the paragraph above we will send them to a previous page they came from with -1, if we will put -2 it will send them to steps back; with positive number we will send them forward in the history of their browsing our website 

  <p onClick={() => navigate("/")}>Go home</p>
// if we pass a URL as an argument to navigate() we will send a user to this specific URL

// of course navigate() can be used not only with the user events, for example we can send them to a specific URL after a certain period of time. let's say after 5 seconds we send them to home route:
setTimeout(() => { navigate('/') }, 5000)
   
```

---

## Nested navigation 

If we need to build a nested routing we can easily do it with "extending" a certain route inside the component which is rendered within this route. 

In the following example we have a route 'topics' defined in the parent component `NestingExample`. This route once hit renders component `Topics` which has it's own route with the value of ":topicId" which is a placeholder for whatever will come. We have 3 `Link` elements inside `Topics` with values of "rendering","components","props-v-state" and each time one of this `Link` elements will be clicked it will hit the route "topics/rendering", "topics/components" or "topics/props-v-state" respectively and each of them will render the same component `Topic` inside which we can have access to the dynamic part of the route represented by ":topicId" thanks to useParams() hook and use this data to let's say fetch appropriate content from the DB for the topic provided.

> This is the replacement for `<Switch/>` component from `react-router-dom` versions prior to 6.

<iframe src="https://codesandbox.io/embed/react-router-nesting-routes-up2i7?fontsize=14&hidenavigation=1&module=%2Fexample.js&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="React Router - Nesting Routes"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>


We can also hoist all the nested routes into the single route config:

<iframe src="https://codesandbox.io/embed/react-router-nested-routing-with-routes-hoisted-to-app-js-illlu?fontsize=14&module=%2Fsrc%2FApp.js&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="React Router - Nested Routing with routes hoisted to App.js"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

# **Exercise time**

