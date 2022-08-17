# Block 03: Loops

---

<details>
    <summary>🎬 Video: loops screencast</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/GAcZZF8SDZg?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---

<!-- Extra:

<details>
    <summary>🎬 Video: loops classroom workshop</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/CiRVzCbkhb4?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

--- -->

Loops are a way to repeat a certain action(s) a given number of times or based on specified condition.

Loops are used for all kinds of iterations allowing code to be executed repeatedly. After all this is what computers are really good at: repeat lots of things really fast!

The most basic example of the use of a loop would be printing out the numbers from 1 to 10:

```javascript
for (var i = 1; i < 11; i++) {
    //here our loop will start at 1 and go on until our iterator is smaller than 11, running therefore 10 times.
    console.log(i)
}
```

> Question: why did we have to use 11 instead of 10?

## `For` loop

1. We start with the keyword `for`.
2. Then we open and close parentheses.
3. We declare a variable which we use as our iterator, it is commonly called **i** (short for iterator) but it could be called whatever.
4. We assign to it a numeric value which is the starting point of the loop. For our loop to count from **0 to 10 we would assign the value 0** to our variable, and to count from **10 to 0 we would assign the value of 10**.
5. Then we need a condition, our loop should run until this condition is met. Like until our iterator is bigger than a number, or until the iterator is smaller than a number.
6. Of course there is one missing piece of the puzzle, we need to either increase or decrease our iterator in order for the loop to run.

Let’s say we created a loop that in English say:

**start with iterator equal to 0 and run while iterator is less than 10**

This loop will never stop because 0 will always be less than 10 unless we do something about it:

**start with iterator equal to 0, increase by 1 each time and run while iterator is less than 10**

In JavaScript this would be:

```javascript
for (var i = 0; i < 10; i += 1) {
    //run
}
```

So to print out numbers from 0 to 5 it would be

```javascript
for (var i = 0; i < 6; i++) {
    console.log(i)
}
```

And to print our numbers from 5 to 0 we would do the opposite.

```javascript
for (var i = 5; i > -1; i--) {
    console.log(i)
}
```

Here is the syntax for a `for` loop:

```javascript
// we use semicolons to separate the arguments
for ([initialization]; [condition]; [final - expression]) {
    statement
}

var i = 0
for (i; i < 9; i++) {
    console.log(i)
    // more statements
}

//SAME EXAMPLE BUT WITH ACTUAL VALUES...

// we use semicolons to separate the arguments
for (var i = 0; i < 100; i++) {
    console.log(i)
}

//same loop but declaring the variable i outside the loop
var i = 0
for (i; i < 9; i++) {
    console.log(i)
    console.log("hello")
}
```

We can loop through a range of numbers with a step other than 1:

```javascript
for (var i = 0; i < 10; i += 3) {
    console.log(i)
}
```

We can use iterator as an index to loop through the array. In this case we normally use length of the array as a condition to stop the loop so that it will go through the entire array:

```javascript
let fruits = ["kiwi", "orange", "apple", "banana"]
for (var i = 0; i < fruits.length; i++) {
    console.log(fruits[i])
}
```

Looping on the strings is no different from looping on arrays:

```javascript
let foo = "banana"
for (var i = 0; i < foo.length; i++) {
    console.log(foo[i])
}
// => b
// => a
// => n
// => a
// => n
// => a
```

## `While` Loop

The while statement creates a loop that executes a specified statement as long as the test condition evaluates to true. The condition is evaluated before executing the statement.

In other words the loop keeps running until what is inside the parentheses is true.
so if we write:

```javascript
while (10 > 5) {
    //run
}
```

This will run forever because 10 will always bigger than 5.

```javascript
while (condition) {
    //statement
}
```

So in order to make our loop run a set amount of time we can do exactly the same thing we did with the `for` loop although the syntax isn’t identical.

```javascript
var num = 0
while (num < 10) {
    console.log(num)
    num += 1
}
```

A shorter version of += is ++, although keep in mind that unlike += which could be followed by any number, ++ will increase by one each time.
so"

```javascript
var num = 0
num += 1 // is equivalent to
num++
```

Example:

```javascript
var n = 0
var x = 0
while (n < 3) {
    n++
    x += n
}
```

## forEach loop

The forEach loop is one of the simplest examples of **higher order functions**, it can only be used on arrays.

The `forEach` loop expects a function as first argument. Inside the function we can pass one or two arguments. The first is the element of the array and second is the index.

```javascript
var fruit = ["banana", "orange", "pineapple", "coke"]

fruit.forEach(function (item, index) {
    //the first argument of the anonymous function is always the element of the array
    //we are looping through and the second is its index.
    console.log("i am item", item)
    console.log("i am the index", index)
})

//i am item banana
//i am the index 0
//i am item orange
//i am the index 1
//i am item pineapple
//i am the index 2
//i am item coke
//i am the index 3
```

And the same loop written with the arrow function:

```javascript
var fruit = ["banana", "orange", "pineapple", "coke"]

fruit.forEach((item, index) => {
    //the first argument of the anonymous function is always the element of the array
    //we are looping through and the second is its index.
    console.log("i am item", item)
    console.log("i am the index", index)
})

//i am item banana
//i am the index 0
//i am item orange
//i am the index 1
//i am item pineapple
//i am the index 2
//i am item coke
//i am the index 3
```

## for-of loop

`for-of` allows us to run the same code for each value of the array, one by one, from left to right.

This loop works for arrays and strings.

```javascript
var arr = ["apple", "orange", "pineapple", "banana"]

for (var ele of arr) {
    console.log(ele)
}
//apple
//orange
//pinapple
//banana

var val
for (val of ["Hey", 1, 2, 3, "z"]) {
    console.log(val)
}
// => "Hey"
// => 1
// => 2
// => 3
// => "z"
val // => "z"
```

In the same way we can loop through strings:

```javascript
let foo = "banana"
for (var l of foo) {
    console.log(l)
}
// => b
// => a
// => n
// => a
// => n
// => a
```

Eventually with practicing it will be easy for you to choose the best suited loop for every specific case but for now here is a simple cheatsheet to help you:

<img class='full_width' src="https://barcelonacodeschool.com/files/pics/cur_files/choosingLoopForArrays.png">

> Kahoot trivia for the Loops: https://kahoot.it/challenge/?quiz-id=48cb2cff-e343-4b84-aa5f-0bd880e0300d&single-player=true



# Exercise time!
