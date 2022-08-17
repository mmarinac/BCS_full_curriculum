# Array methods

> In many cases we can replace looping through array with one of the suitable methods. However, please do not use them for the "Block 3 Loops" exercises because you need to get confident with loops first. Thanks!

## 👉 map() 👈

The `map()` method creates a new array with the results of calling a provided function on every element in the calling array.

```javascript
var array = [1, 4, 9, 16]

const mapResult = array.map((x) => x * 2)

console.log(mapResult)
// expected output: Array [2, 8, 18, 32]
```

> For all these methods which are taking a callback function as an argument we can either declare it directly inside the parenthesis of a method or declare it separately and pass by name:

```javascript
var array = [1, 4, 9, 16]

let multiply=(num)=>num*2

// pass a function to map
const mapResult = array.map(multiply)

console.log(mapResult)
// [2, 8, 18, 32]
```

## filter()

The `filter()` method creates a new array with all elements that pass the test implemented by the provided function.

```javascript
var nums = [1, 33, 44, 66, 77, 88, 99]

const result = nums.filter((num) => num > 10)

console.log(result)
// expected output: Array [33,44,66,77,88,99]
```

## some()

The some() method tests whether at least one element in the array passes the test implemented by the provided function. It returns a Boolean value.

```javascript
const numbers = [1, 2, 3, 4, 5]

numbers.some((test) => test > 3)
// ==> true
```

## reduce()

This method receives a function which has an accumulator and a value as an argument. It applies the function to the accumulator and each value in the array to return at the end just a single value, for example if you need to get a sum of all elements in the array or multiply them all 😐.

```javascript
const numbers = [1, 2, 3, 4, 5]

numbers.reduce((total, value) => total * value)
// 1 * 2 * 3 * 4 * 5
//==> 120
```

We can also specify the initial value for the combined total:
```javascript
[10,20,30].reduce((total, number) => (total + number), 5)
// 5 + (10 +20 + 30)
//==> 65
```

If we want to reduce an array of objects we have to provide initial total otherwise the math will not work:


```javascript
let product1 = {name: 'Book1', price:10}, 
    product2 = {name: 'Book2', price:20}, 
    product3 = {name: 'Book3', price:30}

let cart = [product1, product2, product3]

let subTotal = cart.reduce((total, product)=>(total + product.price),0)

console.log(subTotal)
// 60
```


## every()

This method tests the array with a function passed as a parameter and returns Boolean true if _each_ element of the array match the test and false otherwise.

```javascript
const myArray = ["a", "b", "c", "d", "e"]

myArray.every((test) => test === "d")
//==> false

const myArray2 = ["a", "a", "a", "a", "a"]

myArray2.every((test) => test === "a")
//==> true
```

```javascript
var curDB = [ ["euro", 1.2], ["gbp", 1.5] ]

// check if every array inside curDB has a value of 'gbp' as the first element
var findCur = curDB.every(c=>c[0]=='gbp')

console.log(findCur)
// false
```

```javascript
const myArray = [
        { id: 1, name: "Vicky" },
        { id: 2, name: "Cristina" },
        { id: 3, name: "Barcelona" },
]

myArray.every((test) => typeof test.id === "number")
//==> true
```

## flat()

The flat() method creates a new array with all sub-array elements concatenated into it recursively up to the specified depth.

```javascript
var arr1 = [1, 2, [3, 4]]
arr1.flat()
// [1, 2, 3, 4]

var arr2 = [1, 2, [3, 4, [5, 6]]]
arr2.flat()
// [1, 2, 3, 4, [5, 6]]

var arr3 = [1, 2, [3, 4, [5, 6]]]
arr3.flat(1)
// [1, 2, 3, 4, [5,6]]

var arr3 = [1, 2, [3, 4, [5, 6]]]
arr3.flat(2)
// [1, 2, 3, 4, 5, 6]

var arr4 = [1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]]
arr4.flat(Infinity)
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

## findIndex() 🙌

The findIndex() method returns an index in an array, if an element in the array satisfies the provided testing function. Otherwise -1 is returned.

We use it as we would `indexOf` in case the values of an array are **not** primitive values like strings or numbers:

```javascript
var curDB = [ ["euro", 1.2], ["gbp", 1.5] ]

// find index of array with first element being 'gbp'
var findCur = curDB.findIndex(c=>c[0]=='gbp')

console.log(findCur)
// 1
```

```javascript
const myArray = [
        { id: 1, name: "Vicky" },
        { id: 2, name: "Cristina" },
        { id: 3, name: "Barcelona" },
]

myArray.findIndex((element) => element.id === 3)
//==> 2

myArray.findIndex((element) => element.name === 'Cristina')
//==> 1

myArray.findIndex((element) => element.id === 7)
//==> -1
```


## find()

The find() method returns a value in the array, if an element satisfies the provided testing function. Otherwise undefined is returned.

```javascript
const numbers = [10, 0, -10, 20, -30, 40, -50]

// find first element which is smaller than 0
console.log( numbers.find(num=> num < 0) )
// expected output: -10
```


```javascript
const myArray = [
        { id: 1, name: "Vicky" },
        { id: 2, name: "Cristina" },
        { id: 3, name: "Barcelona" },
]

myArray.find((element) => element.id === 3)
//==> {id: 3, name: "Barcelona"}

myArray.find((element) => element.name === 'Cristina')
//==> {id: 2, name: 'Cristina'}

myArray.find((element) => element.id === 7)
//==> undefined
```


## reverse()

This method reverses an array. The first element becomes the last, and the last element will be the first.

```javascript
const myArray = ["e", "d", "c", "b", "a"]

myArray.reverse()
//==> ['a', 'b', 'c', 'd', 'e']
```

## flatMap()

The method applies a function to each element of the array and then flatten the result into an array. It combines `flat()` and `map()` in one function.

```javascript
const myArray = [[1], [2], [3], [4], [5]]

myArray.flatMap((arr) => arr * 10)
//==> [10, 20, 30, 40, 50]

// same as running with map() and flat() chained
myArray.map((arr) => arr * 10).flat()
//==> [10, 20, 30, 40, 50]
```

## sort()

With pasing arguments we can use .sort() in a more advanced way for numeric and reversed sorting.

The `array.sort()` method used as it is only sorts the elements of the array alphabetically, however if we pass a function as argument to the sort method we can sort our array in different ways.

```javascript
var sortfunction = (a, b) => {
        //Compare "a" and "b" in some fashion, and return -1, 0, or 1
}
array.sort(sortfunction)
```

When such a function is passed into `array.sort()`, the array elements are sorted based on the relationship between each pair of elements `a` and `b` and the function's return value. The three possible return numbers are: `<0` (less than 0), `0`, or `>0` (greater than 0):

- **Less than 0**: Sort `a` to be a lower index than `b`
- **Zero**: `a` and `b` should be considered equal, and no sorting performed.
- **Greater than 0**: Sort `b` to be a lower index than `a`.

**in other words :**
You need to return 0 if the two elements are equal,
a negative number if `a` should be before `b`
and a positive number if `b` should be before `a`.

To sort an array numerically in ascending order for example, the body of your function would look like this:

```javascript
function sortfunction(a, b) {
        //causes an array to be sorted numerically and ascending
        return a - b
}
```

**Shorthand**.

```javascript
var arr = [1, 88, 66, 55, 66, 666666, 1111111, 3, 5, 3, 5, 5]
//ascending sorting:
arr.sort((a, b) => a - b)
//[1, 3, 3, 5, 5, 5, 55, 66, 66, 88, 666666, 1111111]
```

Sort an array numerically but descending isn't much different, and just requires reversing the two operands `a` and `b`:

```javascript
//descending sorting
arr.sort((a, b) => b - a)
//[1111111, 666666, 88, 66, 66, 55, 5, 5, 5, 3, 3, 1]
```

To randomize the order of the elements within an array, what we need is the body of our `sortfunction` to return a number that is randomly `<0`, `0`, or `>0`, irrespective to the relationship between `a` and `b`. The below will do the trick:

```javascript
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
arr.sort(() => 0.5 - Math.random())
//[1, 4, 5, 3, 8, 6, 2, 7, 0, 9]
```

> Kahoot trivia for the Array methods: https://kahoot.it/challenge/?quiz-id=1850d50f-4169-4777-8ace-9ca53e3cdf15&single-player=true
