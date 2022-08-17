# DOM manipulations

Although we are going to perform all the DOM manipulations with React.js it's worthy to know how we can do it with pure JS partly due to this topic being often used in the technical interviews 🤷‍♀️. Let's see a walkthrough of making a simple ToDo App example. 

Let's first create the stucture of our project. From the Terminal do:

```
mkdir todo_app
cd todo_app
touch index.html styles.css index.js
```

Then open your todo_app folder in the code editor. 

Inside the **`index.html`** file copy the code below to create a simple boilerplate:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Todo App</title>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <!-- next line is going to link the html file with the styles.css file -->
    <link rel="stylesheet" href="styles.css" />
    <link href="https://fonts.googleapis.com/css2?family=Grandstander:ital,wght@0,200;1,100&display=swap" rel="stylesheet">
  </head>
  <body>
    <div class="main" id="main"></div>
    <!-- next line is going to link the html file with the index.js file -->
    <script src="index.js"></script>
  </body>
</html>
```

The div with the id `main`, is the one that is going to contain the list of todos.

Let's add some style in the **`styles.css`** file

```css
html {
  font-family: "Grandstander", cursive;
}

body {
  margin: 0;
  padding: 0;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  flex-direction: column;
}

header h1 {
  font-size: 3rem;
  color: gray;
}

/* ===================   MAIN   =================== */

.main {
  width: 80%;
  max-width: 800px;
  min-height: 50vh;
  max-height: 80vh;
  overflow-y: scroll;
  justify-self: center;
  box-shadow: 5px 10px 18px gray;
  padding: 1em;
}

.todo_container {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  height: 60px;
}

/* ===================   INPUT   =================== */

.inputGroup {
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
}

input {
  border: none;
  outline: none;
  font-size: 1.6rem;
  font-family: "Grandstander", cursive;
  color: gray;
  text-align: center;
}

/* ==================   BUTTONS   ================== */

.button {
  background: none;
  border: none;
  outline: none;
  font-size: 1.6rem;
}

.submit_button {
  font-size: 1.5rem;
  color: palevioletred;
  margin-top: 40px;
  font-family: "Grandstander", cursive;
  transition: 0.6s;
}

.submit_button:hover {
  color: red;
  font-weight: 700;
}

.line_through {
  text-decoration: line-through;
  color: gray;
}

```

In the **`index.js`** file we are going to create an array, with some hardcoded todo items inside and 4 functions:

1. **renderTodos**  => is going to remove the list of todos from the DOM and replace it with the updated one, it will be called after the page load and everytime that we update the array of todos

2. **createDiv**    => is going to create the container of each todo

3. **createButton** => is going to create the buttons that we need inside the todo container

4. **createSpan**   => is going to create the todo text element

Paste the code below in your **`index.js`** file 

```js
const todos = [
  {
    task: "learn javascript",
    completed: false
  },
  {
    task: "learn css",
    completed: false
  },
  {
    task: "learn html",
    completed: false
  }
];

//===============================================================
//======================  RENDER TODOS  =========================
//===============================================================

// renderTodos() will be called after the page has loaded and everytime
// we update the array of todos using the functions:
// createTodo(), deleteTodo(), updateTodo()
// that we are going to create later
function renderTodos() {
  // we access the div that is going to contain the todo list through the id "main"
  // and remove the content using innerHTML.
  // The innerHTML property sets or returns the HTML content (inner HTML) of an element.
  main.innerHTML = "";
  // then we loop through the todos array and we call the createDiv() function on
  // each iteration, if we have 3 objects inside the todos array the forEach loop
  // is going to create 3 div, 1 for each todo
  todos.forEach(ele => {
    createDiv(ele);
  });
}

//===============================================================
//===========  createDiv - createButton - createSpan  ===========
//===============================================================

// we are going to use the next 3 functions to create 3 html elements
// and assign them some css class
// createDiv is the one that is called by renderTodos and the one
// that is going to call createButton and createSpan

function createDiv(obj) {
  // document.createElement is going to create an html element
  // with the tag that we are going to pass as a first argument
  // when we call it, we are using it to create the single todo
  // container (a div)
  // arguments:
  // 1) obj = is the todo object {task: "banana", completed: false}
  const div = document.createElement("div");
  // the setAttribute method is used to assign an attribute to
  // the html tags, when we call it we need to pass as the first
  // argument the name of the attribute that we want to create 
  // and as a second the value of this attribute, we are using it 
  // to assign a "class" and an "id" to the single todo container
  div.setAttribute("class", "todo_container");
  div.setAttribute("id", "todo_container");
  // appendChild is used to append a node to another node, we are
  // using it to append the single todo container to the div with
  // the "id" main, the one that is going to contain the todos list
  main.appendChild(div);
  // below we are calling 2 functions:
  // createButton twice (to create the 2 buttons, one to delete 1 specific todo
  // and the other to update 1 specific todo) and createSpan (to create the span
  // element that is going to contain the name of the todo)
  createButton(div, "✏️", "button", "update");
  createSpan(div, obj, obj.completed && "line_through");
  createButton(div, "🗑", "button", "delete");
}

function createButton(parent, title, classN, action) {
  // passing these arguments we made the function dynamic, so we can use it
  // to create either the delete or the update button
  // arguments:
  // 1) parent = is the parent element where we want to append the button
  // 2) title  = text of the button (in this case an icon)
  // 3) classN = a class name to assign to the button
  // 4) action =  is used to evaluate which function call onclick
  // using createElement we are going to create the button element
  const button = document.createElement("button");
  // through the button constant we are going to use innerHTML to assign a text
  // content to the button
  button.innerHTML = title;
  // we assign a "class" to the button using setAttribute("class", classN)
  // where "class" is the property and "classN" is the value coming from the function
  // arguments
  button.setAttribute("class", classN);
  // to give an onclick event to the button we attach an onclick to the constant
  // button and we pass a function with the argument "event" that we are going to use to get
  // the name of the todo and use it to delete or update the todo.
  // Depending on value of the argument "action" the function will call deleteTodo(event)
  // or updateTodo(event)
  button.onclick = event =>
    action === "delete" ? deleteTodo(event) : updateTodo(event);
  // finally we append button to the "parent" (div)
  return parent.appendChild(button);
}

function createSpan(parent, obj, classN) {
  // this function is going to create the span element that is going to contain the todo text
  // arguments:
  // 1) parent = is the parent element where we want to append the span
  // 2) obj = is the todo object {task: "banana", completed: false}
  // 3) classN = a class name to assign to the span
  // using the createElement method we create a span element
  const span = document.createElement("span");
  // we give a text to the span using innerHTML
  span.innerText = obj.task;
  // we give a class to the span using setAttribute
  span.setAttribute("class", classN);
  // finally we append span to the "parent" (div)
  return parent.appendChild(span);
}
```

At this point if we add an onload event to the opening body tag calling the function `renderTodos()`:

 ```html
<body onload="renderTodos();">
```

and we refresh the browser we should see 3 todos coming from the hardcoded array `todos`.

Next we are going to create 3 functions:

1. **createTodo** => is going to get the text/todo from the input and push a new todo object inside the todos array
2. **deleteTodo** => is going to delete a specific todo from the todos array
3. **updateTodo** => is going to toggle the value "completed" of a specific todo

In order to be able to get the value from input, we need to create an input and a button. In the **`index.html`** file
let's add this code just before the `<script>` tag in the end of your file:

```html
    <div class="inputGroup">
      <input type="text" placeholder="Type something..." id="myInput" />
      <button class='button submit_button' type="button" onclick="createTodo();">Submit</button>
    </div>
```

The input has an "id" that we are going to use to target it.
The button has an `onclick` event that is calling `createTodo()`.

```js
//===============================================================
//=====================  createTodo  ============================
//===============================================================
function createTodo() {
  // the getElementById method is going to return an object
  // that contains data about the element which "id" matches
  // the string that we pass as argument to the method itself.
  // we are going to use it to access the value of the input
  // where the user is going to type the new todo and store
  // it in a constant
  const inputVal = document.getElementById("myInput").value;
  // next we are going to find the index of the todo inside the
  // array of todos, check if it is already present and give
  // some feedback to the user
  const index = todos.findIndex(ele => ele.task === inputVal);
  // if the todo is already present inside the array of todos,
  // we'll return an alert
  if (index !== -1) {
    return alert(`Todo ${inputVal} already present on the list 😕`);
  }
  // in case that the value coming from the input is an empty string
  // we are going also to return an alert
  if (inputVal === "") {
    return alert(`Please provide a valid todo 😕`);
  }
  // otherwise we are going to push, inside the todos array, an object
  // that contain the todo ( coming from the input ) and a completed key
  // initially false
  todos.push({ task: inputVal, completed: false });
  // then we are going to clear the input setting its value to an empty string
  document.getElementById("myInput").value = "";
  // finally, we are going to call the function renderTodos(), that is going
  // to remove all the elements inside the div with the id "main" and append
  // the list of todos (updated with the new todo) to it
  renderTodos();
}
```

The event is an object that contain methods and properties, one of the property is "target" that gives us access to other two properties "previousElementSibling" and "nextElementSibling", both are looking for the same value, the text inside the span tag ( that we are going to get through innerText ):
`e.target.previousElementSibling.innerText` and `e.target.nextElementSibling.innerText`

We are using two different properties because of their position inside the div, that we decided when we called `createButton` and `createSpan` from `createDiv`:
```javascript
      createButton(div, "✏️", "button");
      createSpan(div, obj, obj.completed && "line_through");
      createButton(div, "🗑", "button", "delete");
```

The position inside the div would be like this:

  update      span      delete
  button      text      button

<img src="https://barcelonacodeschool.com/files/pics/cur_files/todopurejs.png" alt="todo">


So when you click on the delete button, the `deleteTodo` function is looking for the previous sibling element through the event and the `updateTodo` function for the next sibling element: 

```js
//===============================================================
//=================  deleteTodo - updateTodo  ===================
//===============================================================

function deleteTodo(e) {
  // we get the text value from the span
  const todo = e.target.previousElementSibling.innerText;
  // we find the index of the text inside the array of todos
  const index = todos.findIndex(ele => ele.task === todo);
  // we splice the todo from the todos array
  todos.splice(index, 1);
  // finally we call render todos
  return renderTodos();
}

function updateTodo(e) {
  // we get the text value from the span
  const todo = e.target.nextElementSibling.innerText;
  // we find the index of the text inside the array of todos
  const index = todos.findIndex(ele => ele.task === todo);
  // we toggle the value of completed 
  todos[index].completed = !todos[index].completed;
  // finally we call render todos
  return renderTodos();
}
```

And here is the final version of this ToDo App: http://undesirable-jewel.surge.sh/

Source code: https://gitlab.com/barcelonacodeschool/todo_app_js_html

# Exercise: 5-digit calculator

With only HTML, CSS and pure JS you have to create a web page with a form and 5 inputs taking data from the user and the values entered could be they could be alfanumeric. Below add a button "Calculate". 

If one of the values entered is not a number then after user clicks button Calculate you should display a message "One or more inputs contain an invalid data". If all the data entered is numbers then display a green message saying "All the inputs are valid". 

Then, there should be the sorting panel with these 5 values and math action between them: `+`, `-`, `*`, `/`. These actions should be applied to the 5 values entered by user. In the same output area there is a sorting feature to sort the numeric values in ascending or descending order. Every time we change the order the final results are also changing. 

Finally there is a third section there we can see the results of these operations step by step. 

<img src="https://barcelonacodeschool.com/files/pics/cur_files/5digitscalc01.png" alt="5-digit calculator" style="width:100%; margin-bottom:2em;">

<img src="https://barcelonacodeschool.com/files/pics/cur_files/5digitscalc02.png" alt="5-digit calculator" style="width:100%">