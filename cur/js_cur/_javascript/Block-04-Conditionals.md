# Block 04: Conditionals

---

<details>
    <summary>🎬 Video: conditionals screencast</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/o8145bP6N70?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---

[Video lesson code snippet](https://gitlab.com/snippets/1970668)

---

<!-- Extra:

<details>
    <summary>🎬 Video: conditionals classroom workshop</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/I91za_75N8Q?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

--- -->

We use conditionals to check if the given condition is met. If the condition is met then the code inside the block will run otherwise it will not.

```javascript
if (18 > 5) {
    console.log("18 is bigger than 5")
}
```

So this code will run because 18 > 5. However the code below will not because 18 is not < 5

```javascript
if (18 < 5) {
    console.log("18 is smaller than 5")
}
```

So if the condition isn’t met simply nothing will happen, the code will not run.

Should we want some code to run also if the condition is not met we can use `else`

```javascript
var age = 13
if (age >= 18) {
    console.log("old enough to drive a car")
} else {
    console.log("sorry, too young")
}
```

## Multiple/nested conditionals

```javascript
var canDrink = false
var person = "Peter"
if (canDrink == true) {
    console.log(`${person} can drink`)
} else {
    console.log(`${person} cannot drink `)
}
```

In case we want to check for more than 2 conditions like `if` and `else` we can use `else if`. Let’s say we want to check if a person is old enough to drive and if the person is old enough to drink, assuming that the respective ages are 16 and 21.

```javascript
var age = 19
if (age >= 21) {
    console.log("can drink")
} else if (age >= 16) {
    console.log("can drive")
} else {
    console.log("too young for either.")
}

var age = 12
var haveDrivingLicense = false
if (age >= 18) {
    if (haveDrivingLicense === true) {
        console.log("good to drive")
    } else if (haveDrivingLicense == false) {
        console.log("go to driving school")
    }
} else {
    console.log("far too young!")
}

var person_can_drive = undefined
var person = "mike"
var personAge = 19
if (person) {
    if (personAge >= 18) {
        person_can_drive = true
        if (person_can_drive) {
            console.log(`${person} can drive`)
        }
    }
}
//mike can drive

var peterAge = 15
if (peterAge >= 14) {
    console.log("peter can go to see an horror movie")
} else if (peterAge < 14) {
    console.log("peter is too young to watch horror movies")
}
//peter can go to see an horror movie

var arr = ["apple", "orange", "pineapple", "banana"]
if (typeof arr == "object") {
    if (arr.length > 3) {
        console.log(`
                      the variable arr is of typeof ${typeof arr} 
                      and it's length is more than 3`)
    }
}
//the variable arr is of typeof object and it's length is greater than 3
```

## Ternary operator

The ternary operator is a shorter but less readable way to write if statements.

```javascript
var num = Number(prompt("enter a number"))
var fixed = 10

num > fixed
    ? document.write(`<h1>${num} is bigger than ${fixed}</h1>`)
    : document.write(`<h1>${num} is smaller than ${fixed}</h1>`)
```

It consists of condition followed by "?", first option and second option devided by the ":"

If you only have one conditional option you can use this syntax:

```javascript
num > fixed && console.log(`${num} is bigger than ${fixed}`)
```

## Boolean Operators

A JavaScript Boolean represents one of two values: **true** or **false**.

If is not one of these two then it’s not a boolean.

“true” for example is not a boolean, it is a string, and so is “false”. So only **true** or **false** with no quotation marks are booleans. Meaning if we will put a boolean into the condition it will be always evaluated to it's value such is `true` or `false`

```javascript
var foo = true
var bar = false

var num
if (num) {
    console.log("num is true")
} else {
    console.log("num is false")
    // num is false since it's undefined and undefined equals to false
}

var num = 0
if (num) {
    console.log("num is true")
} else {
    console.log("num is false")
    // num is false since it's 0 and 0 equals to false
}

var num = 9
if (num) {
    console.log("num is true")
} else {
    console.log("num is false")
    // num is true since it's defined
}

var x = false
if (x) {
    console.log("x is true") // this code is not executed because x is declared as false
}
```

### Now you can create an infinite loop!

```javascript
while (true) {
    console.log("infinite loop, this will crash your browser!")
}
```

> Try this code:

```javascript
!true
!!true

var lives = 0
var gameOver = false
if (lives < 1) {
    gameOver = true
    console.log("GAME OVER")
}
```

## Truthy and falsy values

Sometimes we need to check if data is truthy or falsy, and it doesn't have to be boolean `true` or `false`. Falsy values can be seen as vaguely "empty" and truthy are values which are not empty in this sense. Although empty object and array are considered truthy as well. 

There are some types of data in JavaScript which are not boolean `true` or `false` 

These evaluate to `true`:

```javascript
    if (true) // boolean true
    if ({}) // any object
    if ([]) // any array
    if (42) // any number except for zero
    if ("any non-empty string") // any string which is not empty
```

These evaluate to `false`:

```javascript
    if (false) // boolean false
    if (null) // null
    if (undefined) // undefined
    if (0) // zero
    if (NaN) // NaN
    if ('') // empty string
    if ("")
```

Let's say we want to have a function which prints airplane boarding pass, we do not care what would be the name of a passenger but we need to make sure that we have the name -- hence we can't print a boarding pass for unknown passenger. In this case we can just check the `passengerName`  for truthyness, if it is empty it will be falsy and we will not print the boarding pass:

```javascript
let printBoardingPass=(passengerName,seatNumber)=>{
    if(passengerName){
        return `Welcome aboard ${passengerName}, your seat is ${seatNumber}`
    } else {
        return `Please provide a passenger's name`
    }
}
```


## Logical operators

### Logical AND (&&)

The following code shows examples of the && (logical AND) operator.

```javascript
var name = "antonello"
var surname = "sanna"
if (name == "antonello" && surname == "sanna") {
    console.log("welcome antonello")
}
```

With the AND operator we are checking multiple conditions and it evaluate to true only if both conditions are met. So for example the below code will not evaluate to true because not both conditions are true.

```javascript
var name = "antonello"
var surname = "smith"
if (name == "antonello" && surname == "sanna") {
    console.log("welcome antonello")
}
```

> We can chain more than two conditions with logical operators.

### Logical OR (||)

The following code shows examples of the `||` (logical OR) operator. Unlike the && operator with the `||` operator only one of the conditions need to be true in order for the statement to evaluate to true. So the below example will evaluate to true because at least one the conditions are true.

```javascript
var name = "antonello"
var surname = "smith"
var age = 111
if (name == "antonello" || surname == "sanna" || age == 35) {
    console.log("welcome antonello")
}
```

### Logical NOT (!)

The following code shows examples of the ! (logical NOT) operator.

```javascript
n1 = !true // returns false
n2 = !false // returns true
n3 = !"Cat" // returns false
```

For the booleans it changes the value to the opposite, from `true` to `false` and vice versa. For other values it converts them to boolean `true` or `false` based on them being truthy or falsy initially and reverse the value:

```javascript
let foo = 10 // 10 is truthy value
!foo // converts foo to boolean and since 10 is truthy it makes it boolean true
// then reverse the meaning to the opposite, false in this case
console.log(!foo)
// false
```

In case of assignments logical OR will choose the truthy value. Try this code:

```javascript
var v1 = 1
var v2
var v3 = v2 || v1

if (v2) {
    v3 = v2
} else {
    v3 = v1
}
```

If you want to choose right operand only if left operand is null or undefined you can use nullish coalescing operator `??`:

```javascript
null ?? 10 // 10
undefined ?? 10 // 10
false ?? 10 // false
0 ?? 10 // 0
"" ?? 10 // ""
2 ?? 10 // 2
"z" ?? 10 // "z"
true ?? 10 // true

// for example with assignment:
let foo = null ?? 10
// the value of foo would be 10 but
let foo = false ?? 10
// the value of foo would be boolean false
```

Compare it to `||` which will use right operand in case of _any_ falsy value on the left:

```javascript
null || 10 // 10
undefined || 10 // 10
false || 10 // 10
0 || 10 // 10
"" || 10 // 10
2 || 10 // 2
"z" || 10 // "z"
true || 10 // true
```

### Logical OR assignment `||=`

It only assigns operand on the right if operand on the left is falsy:

```javascript
var name = "Jack",
    lastname = ""

name ||= "Bob"
console.log(name)
// expected output: Jack

lastname ||= "Lastname is empty string"
console.log(lastname)
// expected output: "Lastname is empty string"
```

### Logical nullish assignment `??=`

This one is similar to `||=` except it only assign the value of the right operand if operand on the left is `null` or `undefined`:

```javascript
var name = "Jack",
    lastname = "",
    age

name ??= "Bob"
console.log(name)
// expected output: Jack

lastname ??= "Lastname is empty string which is falsy but not null or undefined"
console.log(lastname)
// expected output: ""

age ??= 50
console.log(age)
// expected output: 50 since age is undefined
```

> Kahoot trivia for the Conditionals: https://kahoot.it/challenge/?quiz-id=86e09057-e16d-491a-8ed5-ff4f6ce9e270&single-player=true

# Exercise time!
