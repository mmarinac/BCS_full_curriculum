# React 09: Using External Components

---

<details>
    <summary>🎬 Video: React -- external components</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/u_poDlLX2lg?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

The same way we import our own components we can also import external components from the libraries written for React.

There are tons of super useful third parties components.

Even well-known CSS/jQuery libraries such as Bootstrap and Semantic UI have their equivalent for React which we can use. 

When we want to use an external library we always prefer the special React version if available compared to a version which is supposed to work for the HTML pages. This is a better choice for us to use than the standard version because it is jQuery-free and using jQuery along with React is not a good idea as JQuery manipulates he DOM directly and makes it harder for React to detect changes as React uses its own virtual DOM.

For example, this is a classic CSS/jQuery Semantic UI library -- https://semantic-ui.com -- and here is React Semantic UI which we should use -- https://react.semantic-ui.com

Please note that you can still mix it with the original Semantic UI CSS, and in fact when using a component with no JS attached such as a button or an input field the original CSS library may still be the better option or at least the most straightforward to use.

> We have created a super simple reusable component for you -- https://www.npmjs.com/package/react-easy-css-grid-layout -- it is a Grid component which can help you to create a Grid container with a specific number of columns and their width. Feel free to try it out as with this simple example it could be easier to understand how we use external components...

## Introducing Semantic UI react 

Semantic UI is a great looking and easy to use library for React, it has tons of components ready to use, like menus, dropdowns, buttons etc…

[Semantic UI React docs](https://react.semantic-ui.com)

You can freely browse through the component where in need of one and just grab it and place it in your application.

In most cases all we need to do is to copy the component from the site editing to fit our needs.

Like all libraries in order for us to use it we need to install it.

```
npm install semantic-ui-react semantic-ui-css
```

Then import Semantic UI styles at the top level of your app (index.js):

```
import 'semantic-ui-css/semantic.min.css'
```

[Semantic UI React - Get Started](https://react.semantic-ui.com/usage)

We are going to build a form using an input component and a button component coming from Semantic UI React.

Create a new React app, install Semantic UI React and import the css file inside index.js

Lets replace the content of App.js for this:

```javascript
import './App.css';

function App() {
  return (
    <div className="container">
      <form></form>
    </div>
  );
}

export default App;
```

Lets give some basic styles to it, replace the content of App.css for this:

```css
.container {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

form {
   width: 30%;
   border: 1px solid lightslategray;
   padding: 2rem;
   display: flex;
   flex-direction: column;
}
```

If you run it, in the browser you should see a white page with an empty square in the center.

Now from Semantic UI React we are going to search for an input, we are going to get the first from the inputs page:

[Semantic UI React - Inputs](https://react.semantic-ui.com/elements/input/)

<img src="https://barcelonacodeschool.com/files/pics/cur_files/semantic-ui-input1.png" style="width: 80%;">

If you click on try it, it should open a menu with the code of this component

<img src="https://barcelonacodeschool.com/files/pics/cur_files/semantic-ui-input2.png" style="width: 80%;">

from this code we need the import part ( each Semantic UI component has to be imported from Semantic UI) and we also need the component itself, after adding them to App.js, the code looks like this:

```javascript
import { Input } from 'semantic-ui-react'
import './App.css';

function App() {
  return (
    <div className="container">
      <form>
         <Input focus placeholder='Search...' />
      </form>
    </div>
  );
}

export default App;
```

In the browser, it should be the result:

<img src="https://barcelonacodeschool.com/files/pics/cur_files/semantic-ui-input3.png" style="width: 80%;">

The same way we got the input, we are going to get the button, from the button page:

[Semantic UI React - Buttons](https://react.semantic-ui.com/elements/button/)

we are going to get the first one, like the input it has to be imported, then it can be included in the render, App.js now looks like this:

```javascript
import { Input, Button } from 'semantic-ui-react'; // we can import the components in the same line
import './App.css';

function App() {
  return (
    <div className="container">
      <form>
         <Input focus placeholder='Search...' />
         <Button>Submit</Button>
      </form>
    </div>
  );
}

export default App;
```

in the browser it should look like this:

<img src="https://barcelonacodeschool.com/files/pics/cur_files/semantic-ui-input6.png" style="width: 80%;">

Between the input and the button there is no space, we could add some style to the input to give it some margin bottom, to check if there is a style prop on the props list of the input we can go at the top of the component page and click on the props button:

<img src="https://barcelonacodeschool.com/files/pics/cur_files/semantic-ui-input4.png" style="width: 80%;">

a list should appear:

<img src="https://barcelonacodeschool.com/files/pics/cur_files/semantic-ui-input5.png" style="width: 80%;">

there is a className prop available, lets add it to the component Input:

```javascript
<Input className='search-input' focus placeholder='Search...' />
```

in App.css add:

```css
.search-input {
  margin-bottom: 2rem;
}
```

