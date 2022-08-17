# Block 02: Arrays and Strings

---

<details>
    <summary>🎬 Video: arrays and strings screencast</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/uNIuzvytFus?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---

<!-- Extra:

<details>
    <summary>🎬 Video: arrays and strings classroom workshop</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/AC9prFebNpU?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

--- -->

In JavaScript an array is a special type of variable, which can hold more than one value at a time. Array is basically a list of items separated by a comma.

If you have a list of items (a list of names, for example), storing the names in separate variables could look like this:

```javascript
var names = [(name1 = "antonello"), (name2 = "paulina"), (name3 = "george")]
```

Declaring these names in the array, as a list of names, is simple as that:

```javascript
var names = ["antonello", "paulina", "george"]
```

The most common way to define an empty array is using the array literal.

Defining an array using the array literal definition is as simple as creating a variable and assigned to it as a value a set if open and closed **square brackets**. `[]`

```javascript
var myArray = [] //this is now an empty array
var fruits = [] //this is also an empty array
```

Arrays have several properties, the most commonly used are **length** and **index**.

## **Length**

The **length** property tells us how many elements are inside the array, for example:

```javascript
var arr = ["zero", "one", "two"]
console.log(arr.length) //3
```

## **Index**

The **index** is the position of an element inside the array, starting from zero.

```javascript
var arr = ["banana", "orange", "strawberry"]

console.log(arr[0]) //banana
console.log(arr[1]) // orange
console.log(arr[2]) // strawberry
```

You can use the index property of the array to add or replace elements in the array. Let’s go back to our empty array of the previous example:

```javascript
var myArray = []
myArray[0] = "apple"
//our previously empty array has now one element inside it at the index of 0.
// now try:
console.log(myArray)
```

You can add as many elements as you'd like using this syntax:

```javascript
var myArray = []
myArray[0] = "new element"
myArray[1] = "banana"
myArray[2] = "car"
console.log(myArray)
```

Bare in mind that if you try adding an element to an index that you have previously assigned to another element it will overwrite it.

```javascript
var myArray = []
myArray[0] = "new element"
console.log(`myArray after adding the first element to index 0 ${myArray}`)
myArray[0] = "banana"
console.log(`myArray after adding the second element to index 0 ${myArray}`)
```

## Destructuring arrays

Destructuring is an elegant way of extracting data from arrays and objects in JavaScript.

Destructuring arrays is based on the index or position of the items inside arrays. In the below example we are taking the first property from the array and assigning to a variable called `one`.

The reason we are grabbing the first element of the array is because we are passing only one in the const `one` declaration.

```javascript
const people = ["Peter", "Robert", "Jenny"]
const [one] = people
console.log(one)
```

In the following example we will `console.log` the second element of the same array.

```javascript
const people = ["Peter", "Robert", "Jenny"]
const [one, two] = people
console.log(two)
//Robert
```

Of course the fact that we called them `one` and `two` has no effect on how it works.

```javascript
const people = ["Peter", "Robert", "Jenny"]
const [banana, orange] = people
console.log(orange)
//Robert
```

### Generating arrays of numbers

Generating an array of consecutive numbers from 0 with a given number of elements (length of array):

```javascript
let numbers = [...Array(5).keys()]
console.log(numbers)
// [(0, 1, 2, 3, 4)]
```

Generating an array of numbers with custom initial number and custom step:

```javascript
// let's say we want to have an array of ten numbers starting from 5 with a step of 3
let start = 5
let arrLength = 10
let step = 3
let numbers = Array.from(Array(arrLength), (x, index) => start + index * step)
console.log(numbers)
// [(5, 8, 11, 14, 17, 20, 23, 26, 29, 32)]
```

## Array methods

## array.splice()

There are several methods used to remove items from an array, one of the most useful is **array.splice()**.

Array.splice takes up to 2 arguments, the first is the **index that you want to start removing from** and the second is **how many elements you want to remove.**

So for instance in the below example we want to stat from index 1 (element “two”) and we want to remove 2 elements:

```javascript
var list = ["one", "two", "three", "car", "banana"]
list.splice(1, 2)
console.log(list)
//["one", "car", "banana"]
```

If you want to remove all elements in the array, you can start from the zero index (which is the first element) and pass `array.length` as the second argument like so:

```javascript
var list = ["one", "two", "three", "car", "banana"]
list.splice(0, list.length)
console.log(list)
//[]
```

Another way to achieve the same result is starting from 0 and not passing the second argument at all, in which case it will default to array.length.

```javascript
var list = ["one", "two", "three", "car", "banana"]
list.splice(0)
console.log(list)
//[]
```

If you just want to remove the last element of the array you can just pass one argument `-1`

```javascript
var arr = ["tv", "dvd", "cd", "vhs", "minidisc"]
arr.splice(-1)
console.log(arr)
//["tv", "dvd", "cd", "vhs"]
```

In the same way you can remove any number of items to remove starting from the last one by giving a number of items with `-` sign as an argument:

```javascript
var arr = ["tv", "dvd", "cd", "vhs", "minidisc"]
arr.splice(-2)
console.log(arr)
//["tv", "dvd", "cd"]
```

## array.push()

In order to add new elements to the array without worrying about the index we can use the built-in method `array.push()`.

The `push()` method adds new items to the end of an array, and returns the new length.

```javascript
var arr = []
arr.push("apple")
//1 -> the length of the array

var arr = []
arr.push("antonello", "george", "mike")
//3 -> the length of the array
```

## array.pop()

`.pop()` method removes the **last** element from an array and returns it back, the original array is modified:

```javascript
let fruits = ["apple", "orange", "kiwi"]
fruits.pop()
// "orange"
fruits
// (2) ["apple", "orange"]
```

## array.shift()

`.shift()` method removes the **first** element from an array and returns it back, the original array is modified:

```javascript
let fruits = ["apple", "orange", "kiwi"]

fruits.shift()
// "apple"
fruits
// (2) ["orange", "kiwi"]
```

## array.unshift()

`.unshift()` method adds one or several elements **in the beginning** of an array and returns the length of modified array:

```javascript
let fruits = ["apple", "orange", "kiwi"]

fruits.unshift("banana", "watermelon")
// 5
fruits
// (5) ["banana", "watermelon", "apple", "orange", "kiwi"]
```

## array.concat()

The `**concat()**` method is used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.

```javascript
var arr1 = ["a", "b", "c"]
var arr2 = ["d", "e", "f"]

var arr3 = arr1.concat(arr2)

// arr3 is a new array [ "a", "b", "c", "d", "e", "f" ]
```

While `push` alters the array that invoked it, `concat` returns a new array with the original array joined with the array/s or value/s that were provided as arguments. There are a couple of things to note about `concat` and how it creates the returned array. Both strings and numbers are copied into the array, which means that if the original value is changed, the value in the new array will be unaffected.

```javascript
var arr = []
arr.push("hello")
//1
console.log(arr)
//["hello"]
var arr2 = []
arr2.concat("hi")
//["hi"]
console.log(arr2)
//[]
arr2 = arr2.concat("hey there")
//["hey there"]
console.log(arr2)
//["hey there"]
var arr = ["Hello", "How", "are", "you", "?"]
var arr2 = arr.concat()
console.log("arr", arr)
console.log("arr2", arr2)
//arr (5) ["Hello", "How", "are", "you", "?"]
//arr2 (5) ["Hello", "How", "are", "you", "?"]
arr2[0] = "banana"
console.log("arr", arr)
console.log("arr2", arr2)
//arr (5) ["Hello", "How", "are", "you", "?"]
//arr2 (5) ["banana", "How", "are", "you", "?"]
```

## array.indexOf()

The `indexOf` method is used to fetch the index of the array’s element by it’s name.

```javascript
var arr = ["mike", "jason", "peter"]
console.log("index of mike", arr.indexOf("mike"))
console.log("index of jason", arr.indexOf("jason"))
console.log("index of peter", arr.indexOf("peter"))
//index of mike  0
//index of jason 1
//index of peter 2
```

Not only we can use the `indexOf` method to find out the index of a specific element by its name, but we can also use it to find out if the element is in the array at all.

When we call the `indexOf` method it returns the index of the element if it finds it, and if it doesn't it will **always** return -1:

```javascript
var arr = ["mike", "peter", "john"]
console.log(arr.indexOf("i am not in the array"))
console.log(arr.indexOf("mike"))
console.log(arr.indexOf("banana"))
console.log(arr.indexOf("coca cola"))
console.log(arr.indexOf("john"))
console.log(arr.indexOf("peter"))

//-1
// 0
//-1
//-1
// 2
// 1
```

## array.includes()

Similarly to `indexOf` we have the method `array.includes`, which is used to determine whether the element is present in the array or not.

```javascript
var arr = ["jason", "george", "antonello"]
arr.includes("antonello")
//true

var arr = ["zero", "one", "two", "three", "four", "five"]
console.log(!arr.includes("zero"))
console.log(arr.includes("zero"))
console.log(arr.includes("banana"))
console.log(arr.includes("five"))
//false
//true
//false
//true
```

## **arr.sort()**

`Array.sort` is a built-in JS method that allows effortlessly to sort the elements of the array alphabetically.

In order to use it all we need to to is to call the `.sort` method on our array.

```javascript
var arr = ["f", "h", "z", "t", "q", "a", "s", "f", "g", "o"]
arr.sort()
//["a", "f", "f", "g", "h", "o", "q", "s", "t", "z"]
```

# Strings

Strings also share the length property of the array

```javascript
var fruit = "banana"
console.log(fruit.length)
console.log(fruit[0])
console.log(fruit[1])
console.log(fruit[2])
console.log(fruit[3])
console.log(fruit[4])
console.log(fruit[5])
//6
//b
//a
//n
//a
//n
//a
```

## STRING METHODS

Some useful built-in methods of strings are `string.split()` and `array.join()` although is not a string method but most often is used when we work with strings.

## string.split()

```javascript
var myStr = "I-am-too-young-to-drive-a-car"
console.log(myStr.split("-"))
//(8) ["I", "am", "too", "young", "to", "drive", "a", "car"]
console.log(myStr)
//I-am-too-young-to-drive-a-car
```

As you can see `string.split()` does not affect the original string, so should you want to use the “split” string you need to reassign it

```javascript
var myStr = "I-am-too-young-to-drive-a-car"
myStr = myStr.split("-")
console.log(myStr)
//["I", "am", "too", "young", "to", "drive", "a", "car"]
```

However our string still isn't very useful, in order to have a nicely formatted string we need to combine the method `split` with `string.join()` passing an empty space as argument.

## array.join()

Let’s see in steps what is happening.

```javascript
var myString = "I_love_eating_apples"

console.log("myString", myString)

var mySplitString = myString.split("_")

console.log("mySplitString", mySplitString)

var mySplitAndStringJoinedWithNoArgument = myString.split("_").join()

console.log(
    "mySplitAndStringJoinedWithNoArgument",
    mySplitAndStringJoinedWithNoArgument
)

var splitStringAndJoinedString = myString.split("_").join(" ")

console.log("splitStringAndJoinedString", splitStringAndJoinedString)
//myString I_love_eating_apples

//mySplitString (4) ["I", "love", "eating", "apples"]

//mySplitAndStringJoinedWithNoArgument I,love,eating,apples

//splitStringAndJoinedString I love eating apples
```

Beside that you might find these string methods to be useful:

## string.startsWith()

To check if the string starts with some character(s)

```javascript
var foo = "banana"

foo.startsWith("b")
// true
foo.startsWith("z")
// false
```

## string.includes()

To check if the string contins a specific character(s)

```javascript
var foo = "banana"

foo.includes("z")
// false
```

## string.toUpperCase()

To make a string into uppercase. Is not modifying original string.

```javascript
var foo = "banana"

foo.toUpperCase()
// "BANANA"
```

## string.toLowerCase()

To make a string into lowercase. Is not modifying original string.

```javascript
var foo = "banana"

foor.toLowerCase()
// "banana"
```

## string.charAt()

To get back a character at specific position/index.

```javascript
var foo = "banana"

foo.charAt(0)
// "b"
```

## string.slice()

To get back the characters from a string, takes 1 or 2 arguments, with one argument returns characters starting from the provided index, with 2 arguments returns characters from the first argument/index till second argument/index. Is not modifying original string.

```javascript
var foo = "banana"

foo.slice(1)
//"anana"
foo.slice(0, 3)
//"ban"
```

## string.replace()

To replace the first instance of a given character(s) with the value of the second argument, is not modifying the initial string

```javascript
var foo = "banana"

foo.replace("a", "z")
// "bznana"
```

## string.replaceAll() (node version 15.0.0 and higher)

To replace all instances of a given character(s) with the value of the second argument. Is not modifying the initial string.

```javascript
var foo = "banana"

foo.replaceAll("an", "zz")
// "bzzzza"
```

## string.repeat()

To repeat a string a given number of times

```javascript
var foo = "banana"

foo.repeat(2)
// "bananabanana"
```

# **Template literals**

Template literals are string literals allowing embedded expressions. You can use multiline strings and string interpolation features with them. They were called "template strings" in prior editions of the ES2015 specification.

Let’s see the same example written with the older syntax and with the new one to see the benefits of the template literal approach.

Older approach:

```javascript
var name = "antonello"
var surname = "sanna"
var age = 35

console.log(
    "Mr." + surname + " " + name + " is" + " " + age + " " + "years old"
)
```

Template literal:

```javascript
var name = "antonello"
var surname = "sanna"
var age = 35
console.log(`Mr.${surname} ${name} is ${age} years old`)
```

As you can see the latter is a far more convenient way to mix variables with text without having to worry about + signs and also giving us a much more natural way to deal with spacing.

Template literal are straightforward to use, all we need to remember is to use the backticks ` `` ` instead of the traditional " " or ' ' quotes.

And that in order to inject a variable in the sentence we need to wrap them in `${variable_goes_here}`.

> Kahoot trivia for the Arrays and Strings: https://kahoot.it/challenge/?quiz-id=96e36361-175c-4804-993f-6976865fad26&single-player=true

# Exercise time!
