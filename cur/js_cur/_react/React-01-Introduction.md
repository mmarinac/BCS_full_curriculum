# React 01: Introduction

> We strongly recommend to finish JavaScript blocks 1 - 7 exercises before starting with React. Please push all of your JavaScript solutions to GitLab and notify your mentors so we will check them and give you a green light to start with React. Thanks!

> React official documentation: https://reactjs.org

<details>
    <summary>🎬 Video: React -- create-react-app, intro, function components, rendering from the loop, inner functions</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/JNAkrVaFWq4?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

[Sample code from the video lesson](https://gitlab.com/snippets/1968915)

---

React is a JavaScript library used to create single page applications. It's objective is to render a user interface and react to some events. It is:

**Declarative**
React makes it painless to create interactive UIs. Design simple views for each state in your application, and React will efficiently update and render just the right components when your data changes.
Declarative views make your code more predictable and easier to debug.

**Component-Based**
Build encapsulated components that manage their own state, then compose them to make complex UIs.
Since component logic is written in JavaScript instead of templates, you can easily pass rich data through your app and keep state out of the DOM.

**Learn Once, Write Anywhere**
We don't make assumptions about the rest of your technology stack, so you can develop new features in React without rewriting existing code.
React can also render on the server using Node and power mobile apps using React Native.

---

## Introducing JSX

```javascript
const element = <h1>Hello, world!</h1>
```

This funny tag syntax is neither a string nor HTML.

It is called JSX, and it is a syntax extension to JavaScript. We recommend using it with React to describe what the UI should look like. JSX may remind you of a template language, but it comes with the full power of JavaScript. With React we can render UI based on some logic, so it can react on user actions and state of the app.

```javascript
import React from "react"

const App = () => <p>This is React rendering HTML!</p>

export default App
```

---

<iframe src="https://codesandbox.io/embed/react-block-1-1-forked-s4lkn?fontsize=14" title="React Block 1 - 1" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

---

That's several lines of ES6 code, of which one is empty and two are just closing braces by themselves, so hopefully nothing too challenging for you. But what's interesting is the use of HTML, because it's right in the middle there and not surrounded by quotes. And yet it works, which is one of the marvelous things about React: this is called JSX, and when your code gets built by Webpack that JSX automatically gets converted into JavaScript.

Anyway, as you can see JSX looks pretty much like HTML, although there are a few exceptions you'll learn as you progress. Let's take a look at each of the important lines of code:

`import React from 'react'`

loads the React library, which is pretty central to our whole application and thus is required.

`const Detail = () => <p>This is React rendering HTML!</p>`

defines a new React function component with name "Detail". React components can be big (like pages) or small (like a custom component to render breadcrumbs) and they are very flexible.

`export default Detail`

the "export" keyword means this component is being exposed to the rest of our app to use, and "default" means it's the only thing this class will expose.

> Component's name should start with uppercase letter

---

You can put any valid JavaScript expression inside the curly braces in JSX. For example, `2 + 2`, `user.firstName`, or `formatName(user)` are all valid JavaScript expressions.

```javascript
var friend = 'Mike'
<h1>Hello {friend} how are you today? </h1>
```

This would output:

`Hello Mike how are you today?`

---

To get started with React you can install this package which will make a boiler plate for us to work with...

`npm install -g create-react-app`

Once inside the folder where you wish to create the new app run the following command

```javascript
create-react-app nameOfyourApp
cd nameOfyourApp
npm start
```

---

Navigate to `src/App.js`
Delete all content from your App.js
The first thing we need to do in order to use react is to require it, or using ES6 syntax to import it as follows:

`import` your_variable_name' `from` 'the_name_of_the_actual_library'

so in our case the full statement is:

`import React from 'react'`

Another important thing we must do is to export our component so that it's available in our index.js

---

You can use the syntax you learned with express or you can use the ES6 syntax as shown in the example below:

```javascript
import React from "react"
//require React

const App = () => {
  //Create a React function component called App

  var myName = "Luke"
  //make sure you defined your variable outside the return

  return (
    //ALL that you display needs to be inside your return
    <div className="App">
      {/*render a DIV with a h2 inside*/}

      <h2>Welcome to React from {myName}</h2>
      {/* In curly braces we execute ANY valid JS */}
    </div>
  )
}

export default App //Export your component
```

---

<iframe src="https://codesandbox.io/embed/react-block-1-2-forked-kyluj?fontsize=14" title="React Block 1 - 2" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

---

> Important thing to keep in mind is that a React component can only render **one** HTML element at a time, so this will fail:

```javascript
import React from 'react';
const App = () => {
    return (
      <h1>Hello!</h1>
      <p>Welcome to react</p>
      <p>How are you?</p>
    )
  }
export default App;
```

---

> What we need to do is to wrap all the HTML elements we render into one single wrapper element:

```javascript
import React from "react"
const App = () => {
  return (
    <div>
      <h1>Hello!</h1>
      <p>Welcome to react</p>
      <p>How are you?</p>
    </div>
  )
}
export default App
```

---

> But in case we do not want to create this `div` just for the rendering (like if we don't add class to it for the sake of CSS) then we have 3 ways of solving the issue.

> 1. Returning array of JSX elements:

```javascript
import React from "react"
const App = () => {
  return [<h1>Hello!</h1>, <p>Welcome to react</p>, <p>How are you?</p>]
}
export default App
```

---

> 2. Using React Fragments:

```javascript
import React from "react"
const App = () => {
  return (
    <React.Fragment>
      <h1>Hello!</h1>
      <p>Welcome to react</p>
      <p>How are you?</p>
    </React.Fragment>
  )
}
export default App
```

---

> 3. Using empty tag:

```javascript
import React from "react"
const App = () => {
  return (
    <>
      <h1>Hello!</h1>
      <p>Welcome to react</p>
      <p>How are you?</p>
    </>
  )
}
export default App
```

---

## Rendering elements in a loop

If we have multiple elements to be rendered in React like for example an array of names then we need to use a loop in case of React this has to be a map, which is not much different from a forEach loop apart that it has a return.

> For every element rendered from the loop we need to provide a key prop with unique value

<details>
    <summary>🎬 Video: React -- importance of key prop when render in a loop</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/mjZ0ZXLHmKw?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

[Sample code from the video above](https://codesandbox.io/s/importance-of-using-keys-in-react-rendering-from-the-loop-ljs32?file=/src/App.js)

---

```javascript
import React from "react"

const App = () => {
  const names = ["antonello", "mike", "jason", "peter"]

  return (
    <div>
      {names.map((name, i) => {
        return <h1 key={i}> Hello {name}</h1>
      })}
    </div>
  )
}
export default App
```

---

<iframe src="https://codesandbox.io/embed/boring-thunder-jnmud?fontsize=14" title="React Block 1 - 5" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

---

And the more common approach with a function doing mapping and being executed in the rendering part of the component where we pass data into the function:

```javascript
import React from "react"

const App = () => {
  const names = ["antonello", "mike", "jason", "peter"]

  const renderNames = (data) => {
    return data.map((name, i) => {
      return <h1 key={i}> Hello {name}</h1>
    })
  }
  return <div> {renderNames(names)} </div>
}

export default App
```

---

<iframe src="https://codesandbox.io/embed/react-block-1-3-forked-ecb08?fontsize=14" title="React Block 1 - 3" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

---

## Using uuid for generating unique keys

As you have noticed we are using a property "key" for every element rendered in a loop. A “key” is a special string attribute you need to include when rendering lists of elements as it help React ot identify which item was modified, added or removed to re-render it. Using indexes of arrays is a simple way to have those unique keys but it is nor really the best way to do it as it can confuse React.

Inside your project install uuid package with:

`npm install uuid`

Inside your component where you render in a loop (App.js) for the examples above add:

`import { v4 as uuidv4 } from 'uuid'`

And then we can use uuid() to generate a random unique key, so we can easily assign them to our lists and use later in the rendering in case we do not have any other data/ids to use for that:

---

```javascript
import React from "react"
import { v4 as uuid } from "uuid"

const App = () => {
  // some data without anything which could be used for the keys
  const names = ["antonello", "mike", "jason", "peter"]
  // now we will have an array of objects for evey name with id and name itself
  let namesWithIds = names.map((ele) => ({ id: uuid(), name: ele }))

  const renderNames = namesWithIds.map((item) => {
    // and we have a unique key now
    return <h1 key={item.id}> Hello {item.name}</h1>
  })

  return <div> {renderNames} </div>
}

export default App
```

> If you choose not to assign an explicit key to list items then React will default to using indexes as keys.

---

## Rendering images in React

There are 3 ways of rendering images in react depending on if they are local images or remote.

### For the remote images all you need to do is use URL of the image to render it:

```html
<img alt='artsy banana' src='http://artsy-bananas.surge.sh/artsy_bananas_00.png'/>
```

### Local images in `public` folder

You can create a folder for images inside `public` folder and then simply use relative path to render images. For example, if you will make a folder `pictures` inside your `public` folder and put your images there then the relative path from any react component and also from your CSS files (let's say to use the picture as a background image) would be 'pictures/name_of_the_file.jpg':

```js
<img src="pictures/artsy_bananas_05.jpg" alt="artsy banana" />
```

### Local images in `src` folder

However, if you want to use local images as variables to do some logic you will need to import them first one by one in the beginning of your component with all the rest of the `import` statements and then use in render part like so:

```js
import Banana1 from './images/artsy_bananas_00.png'

<img alt='artsy banana' src={Banana1}/>
```

So that we pass the path to the local image file -- in this example the image is inside folder `images` which have to be inside `src` folder.

With importing images first we can treat them as normal variables and, let's say, put them into an array which we can loop or shuffle or use images inside by their indexes how we would normally use items inside and array:

```js
import banana1 from "./images/artsy_bananas_00.png";
import banana2 from "./images/artsy_bananas_01.jpg";
import banana3 from "./images/artsy_bananas_02.jpg";

export default function App() {
  let images = [banana1, banana2, banana3];
  return(
    <div>
    <img src={images[1]} />
        {
      images.map((picture,index)=><img key={index} src={picture}/>)
    }
    </div>
    )
}
```

> It is also possible to import the local image inline with `require` keyword:

```js
<img alt='artsy banana'  src={require("./images/artsy_bananas_00.png")} />
```

<iframe src="https://codesandbox.io/embed/rendering-images-in-react-wujvk?fontsize=14&hidenavigation=1&module=%2Fsrc%2FApp.js&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="rendering-images-in-react"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>


---

## Adding styles to react component

The most straightforward way would be to have your styles in the .css file and import it in the component like so:

```js
import "./styles.css";
```

Then in the .css file you can use all the CSS as you did before with only one exception -- there is no 'class' attribute in React since `class` is a reserved word in JavaScript so instead we need to use `className`.

For example in CSS you want to select all the elements with class `redtext`

```css
.redtext {
  color:red;
}
```

In react you will need to add `className` to those elements instead of `class` in HTML:

```js
<p className='redtext'>This text will be red</p>
```

Another way would be to add styles per component, so they will only be available inside this specific component. To do so we need to create an object with styles and then apply it inline to the target element. In this case all the combined CSS property names written with a `-` in React will be written together with camelCase, for example take a look at this App.js:

```js
export default function App() {
  return (
    <div className="App">
      {/* applying styles from styles.headings */}
      <h1 style={styles.headings}>Rendering images in react</h1>
      {/* applying styles from styles.text */}
        <p style={styles.text}>Remote image by URL:</p>
 
    </div>
  );
}

// creating an object with styles after closing your component
const styles = {
  headings: {
    color:'red',
    backgroundColor:'grey'
  },
  text: {
    color:'orange',
    fontSize:'smaller'
  }
}
```



## Testing React Exercises

<details>
    <summary>🎬 Video: React -- testing exercises</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/Yl8oxLaGN6o?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---

## **Exercise time**
