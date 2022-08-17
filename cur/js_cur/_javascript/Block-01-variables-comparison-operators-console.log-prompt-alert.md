# Block 01: Variables, Comparison operators, console.log, prompt, alert

## Environment setup: Google Chrome

## Code Editor: Sublime Text or Visual Studio Code

> JavaScript full reference: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference

---

<details>
    <summary>🎬 Video: JS -- variables, comparison, data types, console.log</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/eFTdybmnIzs?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---

<!-- Extra:

<details>
    <summary>🎬 Video: JS block 01 classroom workshop</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/dtRiV2ZH61c?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

--- -->

# Variables

A variable is a storage location paired with an associated symbolic name (an identifier), which contains some known or unknown quantity of information referred to as values.

We use the keyword `var` to define a variable, followed by an arbitrary name that we can freely assign to it.

For example:

`var person;`

---

This is a perfectly valid variable declaration, however this variable holds no value.
In order to declare a variable that holds a value we need:

-   the keyword `var`
-   the name of the variables
-   an assignment operator `=`
-   the value that we are assigning to the variable

`var age = 15;`

Now we declared a variable called `age` and we gave it a value of 15.

---

The content of variables can be changed at any moment, you can think of them as placeholders for your data.

`age` was 15 but we can now re-assign it a value of 18:

`age = 18;`

We don't need to use `var` keyword again if we want to reassign a value. With `var` you will redefine a variable again.

You can use variables for mathematical operations, a bit like in algebra.

---

So if you have a variable called `apple` that holds a value of 2 and another variable called `appleTwo` that holds a value of 5, you could sum them up, and for example assign their sum to a third variable called `basket` that holds their sum:

```javascript
var apple = 2
var appleTwo = 5
var basket = apple + appleTwo
```

> To test all of these snippets you should use Google Chrome. Open a new empty tab in Chrome and press Option+Command+J on Macs or Shift+Control+J on Windows. Then select _Console_ tab and you will have a JS console. Now start writing your JS code there. To create a new line press Shift+Enter. To run the code press Enter. To go through the history of all the code you executed in the console simply press Up or Down arrows on your keyboard.

So now our basket holds a value of 7 as you may expect.

---

Another example:

```javascript
var rent = 800
var shopping = 120
var restaurant = 33
var totalExpenses = rent + shopping + restaurant
```

In the same way you may also subtract variables:

```javascript
var gift = 300
var remainingMoney = totalExpenses - gift
```

> From ES2021 we can add visual separators for big numbers which would be translated into the normal numbers by JS ↓↓↓

```javascript
1_000_000_000
101_475_938.38

let num1 = 123_00
let num2 = 12_300
let num3 = 12345_00
let num4 = 123_4500
let num5 = 1_234_500
```

---

## const & let

`var` respects global and function scope, but not the block scope (inside {}) and we can redefine it as many times is we want. `let` and `const` respect block scope, they sit inside any block defined by a set of curly brackets. We can update `let` but not redefine it in the same scope. And `const` once declared stays the same inside it's own scope, it also should be assigned once declared.

Example:

```javascript
const game = "abc123"
let score = 50
let outcome = false

if (score > 40) {
    let outcome = true
}
```

> Try to change the values in the example above and redefine or update them within outer scope and inside the `if` statement.

Examples:

```javascript
let foo = "banana"
if (true) {
    let foo = "pear"
    console.log(foo) //=> 'pear'
}
console.log(foo) //=> 'banana'
```

OR

```javascript
for (let i = 0; i < 6; i++) {
    console.log(i)
} //=> 1, 2, 3, 4, 5
console.log(i) //=> ERROR!!!

```

## Variable hoisting

In JavaScript you can refer to a variable declared later, without getting an exception.

This concept is known as hoisting. Variables in JavaScript are, in a sense, "hoisted" (or "lifted") to the top of the function or statement. However, variables that are hoisted return a value of undefined. So even if you declare and initialize after you use or refer to this variable, it still returns undefined.

```js
/**
 * Example 1
 */
console.log(x === undefined) // true
var x = 3

/**
 * Example 2
 */
// will return a value of undefined
var myvar = "my value"

;(function () {
    console.log(myvar) // undefined
    var myvar = "local value"
})()
```

The above examples will be interpreted the same as:

```javascript
/**
 * Example 1
 */
var x
console.log(x === undefined) // true
x = 3

/**
 * Example 2
 */
var myvar = "my value"

;(function () {
    var myvar
    console.log(myvar) // undefined
    myvar = "local value"
})()
```

Because of hoisting, all var statements in a function should be placed as near to the top of the function as possible. This best practice increases the clarity of the code.

In ECMAScript 2015, let and const are hoisted but not initialized. Referencing the variable in the block before the variable declaration results in a ReferenceError, because the variable is in a "temporal dead zone" from the start of the block until the declaration is processed.

```javascript
console.log(x) // ReferenceError
let x = 3
```

## console.log

`console.log` is one of the simplest JavaScript methods, the only thing it does is printing out whatever we pass to it as an argument.

In order to execute any JavaScript method we need to write:

-   the name of the method: `console.log`
-   open and close parentheses: `()`

So writing `console.log()` this way would be a perfectly valid way to call the `console.log` method.

However as the purpose of `console.log` is to print out data, it will achieve nothing if we do not pass some data to it.

So to make our `console.log` work, let’s pass an argument. An argument is what goes inside the parentheses, it could be a number, a string, a variable or anything else.

Let’s print out the value of a variable called `age`.

```javascript
var age = 23
console.log(age)
```

We can console.log multiple items at once and in order to do that we can separate them with a comma:

```javascript
var name = "antonello"
var nationality = "italian"
console.log(name, nationality)
```

console.log is super handy when we want to check our code during execution, to see what are the current values of some variables we are using, so it's a first step towards debugging.

<img src="https://barcelonacodeschool.com/files/pics/not_work.jpg" alt="futurama not work">

The values we can assign to variables are not limited to numbers, they could also be strings.

A string in JS stores a series of characters like `"Antonello Sanna"`.
A string can be any text inside _double_ or _single_ straight quotes. So **string** in JS simply put is just a text.

For example `"Antonello Sanna"` and `'Antonello Sanna'` are equivalent.

However please note that you have to be consistent in the quotes you use, for instance
`"Antonello Sanna'` would throw you an error because you started with double and ended with single quotes.

You can combine strings to each other in what is called _string concatenation_:

```javascript
var name = "Antonello"
var surname = "Sanna"
var fullname = name + surname
```

However keep in mind that if you want space in between words you need to add that yourself.

You can either do that by adding an extra space at the end of the string.

    var name = "Antonello "

Or you can add it in the concatenation

    var fullname = name + " " + surname

More examples:

```javascript
var greeting = "hello "
var name = "George "
var question = "how are you today?"
console.log(greeting + name + question)
```

The good thing about using variables instead of hardcoded names is that if the name changes you can keep everything else as it is and still get the correct name printed out:
`name = 'Antonello '`

    console.log(greeting+name+question)

And we can also re-assign values for the variables we used. Note that the type of value could be different from the previous one:

```javascript
name = 100
//and
var foo = 10
foo = "string"
foo = true
foo = null
foo = undefined
```

As you can see every time we assign new value of different data type to the foo variable it’s own data type changes!

This happens because JavaScript is a weakly typed language. It uses dynamic typing, meaning that type of variable is defined by it's value. So what was _string_ before could easily become a _number_ or _boolean_ if we will re-assign corresponding new values to it.

Since `console.log()` output is only visible in the console of DevTools it's not really intended for the final users rather for us, developers. We can print out and check any data with it and clearly see the current value in the process of executing our code so it's invaluable tool to know rather than guess what's going on inside code being executed.

<!-- ![](../pics/not_work.jpg) -->

Although most of the times you will just use `console.log` to print out everything, this method can do much more, for example, try this to print your arrays or objects in a nice table:

```javascript
var array = [1, 2, 3, 4, 5]
console.table(array)
```

With `console.count()` we can count how many times function was called, for example:

```javascript
const follow = (name) => {
    console.count("followers")
    return `${name} is following you`
}

follow("Dan") // followers: 1
follow("Jacob") // followers: 2
follow("Sara") // followers: 3
```

console.assert() only prints to the console if the assertion passed as a first argument is _false_. You will not see it if it's true. The first parameter is what it will check, the second is the message to display.

```javascript
const sum = (n1, n2) => {
    console.assert(n1 + n2 === 10, "Not 10")
}

sum(3, 2) // Assertion failed: Not 10
sum(5, 5) //
sum(10, 0) //
```

And there are more methods hidden in `console.log`, just run `console.log(console)` to see them all!

## Data Types

The latest ECMAScript standard defines eight data types:

Seven data types that are primitives:

1. Boolean, like `true or false`

2. Object for Null, like `null` is an empty value of type 'object', it's not really an object but the result of some bug in the history of js evolution

3. Undefined, like `undefined`

4. Number, like `1, 2, 3, 394.100023123`

5. BigInt, like `2n ** 53n`

6. String, like `'Hello', 'Bye'`

7. [Symbol](https://javascript.info/symbol), like `Symbol('foo'), or Symbol(42)`

and then where is an Object which is not a primitive data type and includes objects, arrays and functions, like `{a:1, b:2}, [1,2,3], ()=>{}`. And there is important idfference betwen primitive data types and objects, the first are always used by the actuall value, and the latter are used by reference.

In order to determine of which type an element is we can use the built-in method `typeof` followed by the element that we are checking the type of.

Unlike `console.log` it is not strictly necessary to use parentheses to execute this method although it would work them as well.

So both of the below examples will give you the same result:

```javascript
typeof 42 // "number"
typeof "abc" // "string"
typeof true // "boolean"
typeof undefined // "undefined"
typeof null // "object"
typeof { a: 1 } // "object"
typeof [1, 2, 3] // "object"
typeof function foo() {} // "function"
typeof NaN // "number"
```

## Comparison operators

The comparison operators are used to compare two or more values to each other.

You can compare for example if a number is greater than another one or if the type of a value is equal to the type of another.

Let’s do a few comparison to understand the operators. You can try them in the console of Google Chrome.

Is 5 bigger than 10?

     5 > 10

Is 100 smaller than 200?

    100 < 200

Is the type of “12" equal to the typeof 12?

    typeof "12" == typeof 12

These comparison will return true or false according to the question asked. One to look out for is the equality operator as there are two of them.

## Abstract equality

    ==

The double equal operator checks for equality however it does so ignoring the type of the element, meaning that “100" and 100 will be considered equal because their type is ignored.

    console.log(3 == "3"); // true.

## Strict Equality

    ===

Strict equality works almost in the same way as the abstract equality although this time the `typeof` is also considered. So not only the values, but also their type should match.

    console.log(3 === "3"); // false.

### Comparison operators list:

```javascript
!= abstract not equal
== abstract equal
!== strict not equal
=== strict equal
< less than
> more than
>= more than or equal
<= less than or equal
```

## Modulus operator

Divides the value of a numeric expression by the value of another numeric expression, and produces the remainder.

```javascript
10 % 2   --> 0
// 2 can stay 5 times inside 10 with no remainder
10 % 3   --> 1
//3 can stay 3 times inside 10 with 1 left as the remainder
15 % 4   --> 3
//4 can stay 3 times inside 15 and 3 is left as the remainder
120 % 32 --> 24
//32 can stay 3 times in 120 leaving 24 as remainder
```

Although the above examples may seem not to be useful, in real life they actually are.

> The most common use for the modulus operator is to check if a number is even or odd. An even number is an integer which is "evenly divisible" by two. ... Zero is an even number because zero divided by two equals zero.

So to check if a number is even all we need to do is using the modulus operator and the number 2 make sure that the remainder is 0.

-   if the reminder is 0 the number is even,
-   otherwise is odd

```
var num = 100;
console.log(num % 2 == 0) // true
    num = 80
console.log(num % 2 == 0) // true
    num = 99
console.log(num % 2 == 0) // false
```

## `prompt()` and `alert()` methods

There is an easy way to capture user's input via built-in method `prompt()`. It display a pop-up window with an input and 2 buttons -- 'Cancel' and 'Ok'. If user clicks "Ok" then we can save the value they entered in the input, if they press "Cancel" then the value would be null. 

Take a look as this example and try it in the console:

```js
let userInput = prompt('Please enter your name')
console.log(userInput)
```

Method `alert()` is displaying a pop-up window with some informational message we can pass into it and "Ok" button which will close the pop-up. Try this example in the console:

```js
let greeting = 'Hello friend, how are you today?'
alert(greeting)
```

## **External JS file**

Let’s see how we can link to external JavaScript file from the HTML page.

Create a new folder 'jsDay1' inside of which you should create 2 files, **index.html** and **index.js.**

Make sure to get the extension right and not to include any spaces.

Then create the standard HTML boiler plate, (write HTML followed by the tab button if you are on Sublime Text) and in your **index.html** file, just before the end of your body tag you can import your `js` file as follows:

    <script src="index.js"></script>

Now to make sure that we have successfully imported the file we can try out a JavaScript built-in method called `alert`.

The `alert` method works similarly to `console.log` although it can also be seen by the user and not only by the developer, because it’s output is not limited to the console.

So in the **index.js** file we write `alert('CONNECTED!!!')`

If you have done everything correctly you should see the message as a pop up in the screen once you reload the **index.html** file in the browser.

`alert` is useful to display data to the user, but what if we need to take data from the user? in that case we can use a built-in method called `prompt`, let's give it a shot!

```javascript
var name = prompt("what is your name?")
alert("Hello " + name + " how are you today?")
```

Another useful JS built-in method is `document.write`. Unlike `alert` this one can be used to write in our HTML page. For instance:

```javascript
var age = prompt("how old are you?")
document.write("You are " + age + " years old")
```

> Kahoot trivia for the Variables: https://kahoot.it/challenge/?quiz-id=9bac11a5-732f-4515-9655-bd6b9f3c68ce&single-player=true

---

## Testing JS exercises

<details>
    <summary>🎬 Video: JS -- testing exercises</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/gshtW9TI0dI?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---

# Exercise time!

## How to use BCS_JS_BOOTCAMP_FILES_TDD_STUDENTS_VERSION

– You should go to the 02_javascript folder

– Then the block you are working on (like block01.js), read the instructions of the exercise and then solve it trying the code in Chrome Dev Tools Console

– Then once you are done and the solution seems to work you can paste it in the appropriate file inside block1 folder (one file per exercise) and test it

– So, there is a folder for each block inside of which we created one file per exercise, if you paste your solution there inside the function it can be tested

– You can find the command to test it in the exercises instructions of block 1
