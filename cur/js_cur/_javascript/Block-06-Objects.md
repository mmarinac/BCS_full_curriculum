# Block 06: Objects

---

<details>
    <summary>🎬 Video: objects screencast</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/FUhClt95IwU?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---

<!-- Extra:

<details>
    <summary>🎬 Video: objects classroom workshop</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/WQuho4W-JJ4?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

--- -->

**Objects are arguably the most important data structure in JavaScript.**

An Object is a collection of properties defined by a key/value pair

**Defining an empty object**

```javascript
var myFirstObject = {}
```

Think of an object as container for many information for example the information of a book or a movie would fit very well inside an object.

```javascript
var book = {
    author: "Stephen King",
    CoverArtist: "Bob Giusti",
    title: "It",
    year: 1986,
    publisher: "Vikings",
}
```

## Syntax to set or retrieve objects properties

Square brackets notation to **get a value** from the object:

```javascript
// nameOfObject.[NameOfKey], such as:

var book = {
    author: "Stephen King",
    CoverArtist: "Bob Giusti",
    title: "It",
    year: 1986,
    publisher: "Vikings",
}

console.log(book["author"])
console.log(book["CoverArtist"])
console.log(book["title"])
console.log(book["year"])
console.log(book["publisher"])

// Stephen King
// Bob Giusti
// It
// 1986
// Vikings
```

Dot notation:

```javascript
// nameOfObject.NameOfKey, such as:

var book = {
    author: "Stephen King",
    CoverArtist: "Bob Giusti",
    title: "It",
    year: 1986,
    publisher: "Vikings",
}

console.log(book.author)
console.log(book.CoverArtist)
console.log(book.title)
console.log(book.year)
console.log(book.publisher)

// Stephen King
// Bob Giusti
// It
// 1986
// Vikings
```

Square brackets notation to **add a value** to the object:

```javascript
// nameOfObject.[NameOfKey] = newValue, such as:

var book = {
    author: "Stephen King",
    CoverArtist: "Bob Giusti",
    title: "It",
    year: 1986,
    publisher: "Vikings",
}

book["author"] = "John Doe"
```

Dot notation:

```javascript
// nameOfObject.NameOfKey = newValue, such as:

var book = {
    author: "Stephen King",
    CoverArtist: "Bob Giusti",
    title: "It",
    year: 1986,
    publisher: "Vikings",
}

book.author = "John Doe"
```

Dot notation is usually the preferred syntax because is faster to write and easier to read however is not as versatile as bracket notation.

With dot notation you **can’t**:

**1: Use variables as keys:**

```javascript
var name = "Antonello"
var surname = "Sanna"
var obj = {}
obj.name = surname
console.log("I am obj created with dot notation", obj)
//I am obj created with dot notation {name: "Sanna"}

var obj2 = {}
obj2[name] = surname
console.log("I am obj2 created with square brackets notation", obj2)
//I am obj2 created with square brackets notation {Antonello: "Sanna"}
```

**2: Use numbers as keys:**

```javascript
var obj = { }
obj[3]='age'
console.log(obj)
//{3: "age"}

var obj = { }
obj.3 = 'age'
//Uncaught SyntaxError: Unexpected number
```

> If you need to check if some key exist in the object, you can use `keyName in objName`. It will return `true` or `false`.

> To remove key:value pair form the object use `delete objName.keyName`

## Destructuring objects:

```javascript
const obj = { name: "antonello", lastname: "sanna", age: 35 }
const { name } = obj
console.log(name)
//antonello
```

Or if you want to assign those values to different variables with different names you can also do this:

```javascript
const obj = { name: "antonello", lastname: "sanna", age: 35 }
const { name: dude } = obj
console.log(dude)
//antonello
```

🤪

### Optional chaining `?.`

While trying to access a property of an object which doesn't exist we will have an error. With optional chaining we can avoid that and instead get `undefined` which will not throw an error and break our code. Compare these 2 examples:

```javascript
let jb = { family: {name: "Jack", lastname: "Black"} }
console.log(jb.family.son) // trying to access property `son` of property `family` which doesn't exist will throw an error

// VM2382:1 Uncaught TypeError: Cannot read property 'son' of undefined
//  at <anonymous>:1:23

console.log(jb.family?.son) // instead with `?.` we will get undefined without breaking the code

// VM2402:1 undefined
```

## Looping inside an Object

### 'For-in' loop

`For-in` loop allows us to run the same code for each property of an object, the `key` will one by one take all the values of each key of the object and do what we need to do to it.

```javascript
var obj = { a: 1, b: 2 }
for (var banana in obj) {
    console.log(
        "I am the key of the object",
        banana,
        "I am the value of the object",
        obj[banana]
    )
}
//I am the key of the object a I am the value of the object
//I am the key of the object b I am the value of the object
```

A bit like you commonly use “i” to loop using a standard `for` loop it is common to use the variable “key” to loop with the `for-in` loop but I wanted to use something totally unrelated (like banana) just to show you that using key is just a convention and nothing more.

```javascript
var obj = { a: 1, b: 2 }
for (var key in obj) {
    console.log(
        "I am the key of the object",
        key,
        "I am the value of the object",
        obj[key]
    )
}
//I am the key    of the object a I am the value of the object
//I am the key    of the object b I am the value of the object
```

> Assign values from one object to another with a loop:

```javascript
var obj = { a: "Mike", b: "George", c: "Antonello", d: "Pedro" }
var newObj = {} //defining an empty object
for (var key in obj) {
    newObj[key] = obj[key]
}

console.log("this is the original obj", obj)

// the output: Object {a: "Mike", b: "George", c: "Antonello", d: "Pedro"}

console.log("this is the newObj", newObj)

// the output: Object {a: "Mike", b: "George", c: "Antonello", d: "Pedro"}

// add new key and value pair to the object with a function
var addMyProperty = function (obj) {
    obj["pedro"] = "likes bananas"
}
addMyProperty(obj)

// same as
function addNewKey(objName) {
    objName["pedro"] = "eats bananas"
}
addNewKey(obj)
```

## Object.keys

Allows us to get all the keys from the object in an array:

```javascript

const foo = {
  a: 1,
  b: 2,
  1: 'a',
  2: 'b',
  3: 'c',
}

Object.keys(foo)
// (5) ["1", "2", "3", "a", "b"]

// and then we can loop on them as with normal array

for(prop of Object.keys(foo)){
console.log(foo[prop])}
// ==> a
// ==> b
// ==> c
// ==> 1
// ==> 2
```

## Object.values

Allows us to get all the values from the object in an array:

```javascript
const foo = {
    a: 1,
    b: 2,
    1: "a",
    2: "b",
    3: "c",
}

Object.values(foo)

// (5)[("a", "b", "c", 1, 2)]
```

## Object.entries

Allows us to get all the entries with key/value pairs from the object in an array:

```javascript

const foo = {
  a: 1,
  b: 2,
  1: 'a',
  2: 'b',
  3: 'c',
}

Object.entries(foo)
// (5) [Array(2), Array(2), Array(2), Array(2), Array(2)]
// 0: (2) ["1", "a"]
// 1: (2) ["2", "b"]
// 2: (2) ["3", "c"]
// 3: (2) ["a", 1]
// 4: (2) ["b", 2]
// length: 5
// __proto__: Array(0)
```

### Generally speaking if you are deleting, adding or modifying properties of the object it is better not to use for... in loop for that because of this:

> A for...in loop iterates over the properties of an object in an arbitrary order (see the delete operator for more on why one cannot depend on the seeming orderliness of iteration, at least in a cross-browser setting).

> If a property is modified in one iteration and then visited at a later time, its value in the loop is its value at that later time. A property that is deleted before it has been visited will not be visited later. Properties added to the object over which iteration is occurring may either be visited or omitted from iteration.

> In general, it is best not to add, modify, or remove properties from the object during iteration, other than the property currently being visited. There is no guarantee whether an added property will be visited, whether a modified property (other than the current one) will be visited before or after it is modified, or whether a deleted property will be visited before it is deleted.

> Source: [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)

You could assign anything to be a property of your object, for example another object:

```javascript
var family = {
    father: {
        name: "Mike",
        age: 44,
        height: 179,
    },
    mother: {
        name: "Jenny",
        age: 40,
        height: 168,
    },
    son: {
        name: "Pablo",
        age: 16,
        height: 165,
    },
}

console.log("the name of the father is", family.father.name)

console.log("the name of the mother is", family.mother.name)

console.log("the name of the son    is", family.son.name)
//the name of the father is Mike
//the name of the mother is Jenny
//the name of the son    is Pablo
```

You could also assign a function to be a property of an object

```javascript
var food = {
    cooking: function (dish) {
        console.log(`Me like cooking ${dish}`)
    },
    eating: function (dish) {
        console.log(`Me like eating ${dish}`)
    },
}
food.cooking("pasta")
food.eating("pizza")
//Me like cooking pasta
//Me like eating pizza
```

The most useful place for an object is inside an array, in fact is a really common pattern to have an array of objects.

```javascript
var movies = [
    {
        title: "the Godfather",
        StoryBy: "Mario Puzo",
        releaseDate: 1972,
    },
    {
        title: "Seven",
        Director: "David Fincher",
        releaseDate: 1996,
    },
    {
        title: "The Naked Gun",
        Director: "David Zucker",
        releaseDate: 1988,
    },
]
```

Of course we can loop inside our array of objects just like we would in any array.

```javascript
var movies = [
    {
        title: "the Godfather",
        Director: "Francis Ford Coppola",
        releaseDate: 1972,
    },
    {
        title: "Seven",
        Director: "David Fincher",
        releaseDate: 1996,
    },
    {
        title: "The Naked Gun",
        Director: "David Zucker",
        releaseDate: 1988,
    },
]

movies.forEach(function (movie) {
    console.log("title", movie.title)
    console.log("Director", movie.Director)
    console.log("releaseDate", movie.releaseDate)
})

//title the Godfather
//Director Francis Ford Coppola
//releaseDate 1972
//title Seven
//Director David Fincher
//releaseDate 1996
//title The Naked Gun
//Director David Zucker
//releaseDate 1988
```

> Kahoot trivia for the Objects: https://kahoot.it/challenge/?quiz-id=5bc9b830-d8ab-43d1-80d9-bf044826aa8b&single-player=true

# Exercise time!
