# Block 05: Functions

---

<details>
    <summary>🎬 Video: functions, part 2 screencast</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/IQb-xOs5Mb0?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---

<!-- Extra:

<details>
    <summary>🎬 Video: functions classroom workshop</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/C27lX8ELhRo?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

--- -->

A function is a "subprogram" that can be _called_ by code external to the function. Like the program itself, a function is composed of a sequence of statements called the _function body_. Values **can** be passed to a function, and the function **can return** a value.

In JavaScript, functions are first-class objects, because they can have properties and methods just like any other object.

Functions could be named by variables, they can be passed as arguments, they could be returned as the output, they could be included in data structures.

What distinguishes them from other objects is that functions can be called. In brief, they are [Function](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Function) objects.

```javascript
let myFirstJavascriptFunction = () => {
  // here comes the function body, which is the block of code to be executed when the function is called.
}
```

First we need to **declare** a function:

```javascript
let sayHi = () => {
  console.log("Hi")
}
```

Then we can **call** the function:

```javascript
sayHi()
```

Functions can run multiple lines of code in one go:

```javascript
let foobar = () => {
  console.log("Hello 1")
  console.log("Hello 2")
  console.log("Hello 3")
  console.log("Hello 4")
  console.log("Hello 5")
}
```

Don't forget to call the function:

```javascript
foobar()
```

Another example:

```javascript
let add = () => {
  console.log(2 + 5)
}
add()
```

In the above example the function adds 2 numbers, however as it is is not very useful, in order for it to be just that, we need to use what’s known as arguments.

## Arguments

```javascript
let add = (a, b) => {
  console.log(a + b)
}
add(2, 5)
add(10, 50)
add(2, 7)
```

As you can see in this example we can now call our function with many different numbers without having to change the actual function, so it’s far more useful!

The arguments are available inside the function by their names. So in this example whatever numbers we are passing to the function, they are we can use them inside by the names of `a` and `b`.

## Return

In order for us to have a ‘real’ output from our function we need to use a return statement.

See the different output from the console with these slightly different functions.

```javascript
let divide = (a, b) => {
  console.log(a / b)
}
divide(100, 4)
//25
undefined
```

```javascript
let divide = (a, b) => {
  return a / b
}
divide(100, 4)
//25
```

As you can see the first function gives back 25 from `console.log()` but also `undefined`.

In the case of the second example it returns 25 but not `undefined` because we included the `return` statement.

```javascript
//declare our function which returns the sum of a + b
let calc = (a, b) => {
  return a + b
}

// assign the value returned by our function to the variable sum
var sum = calc(2, 6)
//now sum is equal to 8
sum
//8
//in the below example on the other end things don't go as well...

let calc = (a, b) => {
  console.log(a + b)
}
var sum = calc(2, 6)
//8
//until here all seems fine, however if we then check what value our
//sum variable holds you see is not what we expect.
sum
//undefined
```

One thing to bare in mind about return is that it ends the execution of our function so if we have more code after the return, that code is not going to be executed!

```javascript
let sayHi = (name) => {
  return "hello " + name
  console.log("I am never going to be executed")
}
sayHi("Pedrito")
//"hello Pedrito"
```

We can use all the stuff we learned so far inside our functions, for example conditionals.

However unlike when we wrote conditionals on their own this time they can be reused over and over again.

```javascript
let checkAge = (person, personAge, minAge, action) => {
  if (personAge < minAge) {
    console.log(`${person} is too young to ${action} `)
  } else {
    console.log(`${person} is old enough to ${action}!`)
  }
}
checkAge("mike", 15, 18, "drive")
//mike is too young to drive

checkAge("mike", 15, 14, "watch horror movies")
//mike is old enough to watch horror movies!

checkAge("Jason", 20, 21, "go clubbing")
//Jason is too young to go clubbing
```

As you can see in the above examples functions make our code reusable hence makes us write less code!

Write less do more, that’s the spirit of a programmer!

We can also have loops inside our functions.

```javascript
let checkArray = (arr) => {
  arr.forEach(function (ele) {
    console.log(typeof ele)
  })
}
var arr = [12, 4, 5, true, "orange"]
checkArray(arr)
//number
//boolean
//string

var arr2 = ["cheese", undefined, 44]
checkArray(arr2)

//string
//undefined
//number
```

Now our function can check the type of each element of whichever array we pass as an argument!

Another way of writing a function would be a legacy ES5 syntax. Compare these two snippets, they are doing exactly the same:

```javascript
//ES6
var sayHi = (name) => {console.log(`Hello ${name}`)}

//ES5
function sayHi(name) {
  console.log(`Hello ${name}`)
}
```

**Extra cool things arrow functions can do:**

1. If you don’t add {} after the argument the arrow function will implicitly return.

These two below examples are equivalent:

```javascript
var doStuff = (name) => {
  return name
}
```

```javascript
var doStuff = (name) => name
```

2. If you have **one argument** in your arrow function you can also omit parentheses, so the second example could be also written as follows:

```javascript
var doStuff = name => name
```

You can also omit the keyword `return` and replace the {} with ():

```javascript
var doIt = (name) => {return name}
```

```javascript
var doIt = (name) => (name)
```

Important:

– We can not use arrow functions as the constructor functions

– Arrow functions bind to the Window object itself rather than to the the container object if using keyword **this**.

Let's see the difference in binding of the keyword this between arrow and regular functions.

```javascript
var obj = {
  arrow: () => {
    console.log(this)
  },
  regular: function () {
    console.log(this)
  },
}
obj.arrow()
//Window {postMessage: ƒ, blur: ƒ, focus: ƒ, close: ƒ, frames: Window, …}
obj.regular()
//{arrow: ƒ, normal: ƒ}
```

## Functions inside functions!

We have seen that we can have conditionals and loops inside our functions, but can we also have a function call inside a function???

Well actually we already did!

when we had our first function `sayHi` it has inside a JavaScript function, namely the built-in method `console.log`.

But we may also call a custom functions from inside our function.

```javascript
let sayHi = (word) => {
  console.log(word)
}
let fun = () => {
  sayHi("Hello")
}
fun()
//Hello

let fun = () => {
  return 1
}
let fun2 = () => {
  var x = fun()
  console.log(x)
}
fun2()
//1
```

```javascript
let mySonExpenses = (games, sodas) => {
  return games + sodas
}
let myExpenses = (rent, grocery) => {
  return rent + grocery
}
let getTotal = () => {
  var mySonExp = mySonExpenses(100, 30)
  var myExp = myExpenses(1200, 230)
  return mySonExp + myExp
}
getTotal()
//1560

//we can write that even shorter by not assigning the return value to variables
//this is called refactoring...

let mySonExpenses = (games, sodas) => {
  return games + sodas
}
let myExpenses = (rent, grocery) => {
  return rent + grocery
}
let getTotal = () => {
  return mySonExpenses(100, 30) + myExpenses(1200, 230)
}
getTotal()
1560
```
## Passing variables between functions

In order to pass variables among functions we need to pass them as arguments. This is very useful because it allows us to have access to our variables and still keep them local.

```javascript
function testTwo (){
    var a = "i am from testTwo"
    testOne(a)
    //here we call the function testOne and we pass the variable a along..
}

function testOne (a){
    console.log('this is test one being called', a)
}

testTwo()
//this is test one being called i am from testTwo
```

Let’s see an example on how we can pass data between functions in a more  useful way.

```javascript
function getData(){
    var name = prompt('enter your name please')
    greetings(name)
}
function greetings(name){
    alert(`Hello ${name} how are you today?`)
}

getData()
//'enter your name please'
//`Hello Antonello how are you today?`
```

This exchange of data is not limited to only two functions, let’s do it with three.

```javascript
function getName(){
    var name = prompt('enter your name please')
    getAge(name)
}
function getAge(name){
    var age =  prompt('enter your age please')
    greetings(name, age)
}

function greetings(name, age){
    console.log(`Hello ${name} you are ${age} years old`)
}

getName()
//Hello Antonello you are 34 years old
```


## IIFE

```javascript
(function foo() {
  console.log("I will run immediately after being declared")
})()
```

An immediately-invoked function expression (IIFE) is a way to execute functions immediately, as soon as they are created.

IIFEs are very useful because they don’t pollute the global object, and they are a simple way to isolate variables declarations since they could be nameless 🤷‍♀️

So this will also work:

```javascript
(function () {
  console.log("I will run immediately after being declared")
})()
```

### Hoisting

Function declarations -- but not the function expressions -- are hoisted in JavaScript, which means they are lifted up in respective scope and could be called before they are declared:

```javascript
/* Function declaration */

foo() // "bar"

function foo() {
  console.log("bar")
}

/* Function expression */

baz() // TypeError: baz is not a function

var baz = function () {
  console.log("bar2")
}
```

> Kahoot trivia for the Functions: https://kahoot.it/challenge/?quiz-id=0f4e2e42-af6d-4f01-bddf-10563dbc7795&single-player=true

# Exercise time!
