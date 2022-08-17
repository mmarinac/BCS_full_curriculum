# Working with numbers 

## Converting to number

### `Number()`

> MDN docs: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number

This method takes an argument and tries to convert it into a number. If it is not possible, it will return `NaN`:

```js
Number('2')
// 2
Number('b')
// NaN
``` 

### isNaN()

This method can tell `true` or `false` if the data is of type 'number' or not. It is especially useful after we tried to perform a conversion of data into a number and want to check if the results are the actual number or `NaN`:

```js
let foo = 10
isNaN(foo)
// false

let bar = NaN 
isNaN(bar)
// true

isNaN(Number('1'))
// false

isNaN(Number('b'))
// true
```



## Random numbers

With `Math` built-in object we have access to many useful methods which we can benefit from when working with numbers. Let's see some of the most useful ones:

> MDN docs: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math

### Math.random()

Often we need to generate a random number and with this method we an do it easily. Every time we call it it will create a random number in the range from 0 to 1, for example:

```js
Math.random()
// 0.8019722737092572
Math.random()
// 0.6923597277764573
Math.random()
// 0.21160558348404535
```

Of course we can save results into a variable and use later as a normal variable:

```js
let randomNumber = Math.random()
console.log(randomNumber)
```

To limit number of decimals after a comma we can use `parseFloat(someNumber.toFixed(howManyDecimals))`, for example:

```js
let randomNumber = Math.random()
console.log(randomNumber)
// 0.08353927858004018
parseFloat(randomNumber.toFixed(2))
// 0.08
```

To generate a random number inside a specific range we can pass extra arguments into `Math.random()`:

```js
Math.random() * (maxNumber - minNumber) + minNumber
// so to generate a random number between 100 and 200 we will run
Math.random() * (200 - 100) + 100
```

The results will be with a bunch of decimals, if we need to have an integer instead we can either wrap this expression into 'parseInt()'' method, which takes a number and returns the integer by dropping the decimals altogether: 

```js
parseInt(Math.random() * (200 - 100) + 100)
// 168
```

or we can round the number up or down based on the math rules with `Math.round()`

## Rounding numbers

### `Math.round()`

If we need to round a number with decimals to an integer according to the math rules we can use `Math.round()`:

```js
Math.round(1.1)
// 1
Math.round(1.9)
// 2
Math.round(1.5)
// 2
```

Other options would be `Math.ceil()` to always round up or `Math.floor()` to always round down:


```js
Math.ceil(1.1)
// 2
Math.ceil(1.9)
// 2
Math.ceil(1.5)
// 2
Math.floor(1.1)
// 1
Math.floor(1.9)
// 1
Math.floor(1.5)
// 1
```

## Biggest/smallest number 

### `Math.max()` and `Math.min()`

These methods return the biggest - `Math.max()` - or smallest - `Math.min()` number out of a list of given parameters or NaN if any of the arguments is not a number and can not be converted to one.


```js
Math.max(-5, 1, 2, 3)
// 3
Math.min(-5, 1, 2, 3)
// -5
```

Of course the most handy use of this method is to find the biggest or smallest number in the array of numbers and to pass the array into these methods we will need to use the spread operator `...` before the name of array:

```js
let numbers = [-5, 1, 2, 3]

// this will return NaN since Math.max will wee numbers as one data item non-convertible into a number
Math.max(numbers)
// NaN

// by spreading the array with ... we "expand" the array from one item into a list of items:
Math.max(...numbers) // for JavaScript this syntax looks like Math.max(-5, 1, 2, 3)
// 3
```

### `Math.abs()`

If we want to find the absolute value of a number regarding of it's sign, we can use `Math.abs()` method:

```js
Math.abs(-3)
// 3
Math.abs(3)
// 3
```


