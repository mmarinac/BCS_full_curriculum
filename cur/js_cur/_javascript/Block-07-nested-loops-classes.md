# Block 07: Nested loops, methods and ES6 classes.

---

<details>
    <summary>🎬 Video: advanced JS block 7 screencast</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/f4qNqc-vS_g?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---
<!-- Extra:
<details>
    <summary>🎬 Video: let, const, arrow func, destructuring, prototype, classes, extends classroom workshop</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/dnWDg3W2OBQ?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

--- -->

## Nested loops

Nested loops are needed in order to fetch data from nested arrays.

```javascript
var arr = [[13,44,55,66],['mike','jason','peter']]
arr.forEach(function(array){
    array.forEach(function(ele){
        console.log(ele)
    })
})

//13
//44
//55
//66
//mike,
//jason,
//peter
```

```javascript
var arr = [
[[['got me!']]]
]

arr.forEach(function(levelone){
 console.log('level 1', levelone)
 levelone.forEach(function(leveltwo){
     console.log('level 2',leveltwo)
     leveltwo.forEach(function(gotYou){
         console.log("gotYou",gotYou)
     })
 })
 
})
//level 1 [Array(1)]
//level 2 [Array(1)]
//gotYou ["got me!"]
```

```javascript
var people = [
{
    males:[
    { name:'mike'  , age:21 },
    { name:'robert', age:19}
    ]
},
{
    females:[
    { name:'jenny'  , age:24 },
    { name:'olga', age:29}
    ]
}
]
people.forEach(function(arr){
    if(arr.males){
        arr.males.forEach(function(male){
            console.log(male.name, male.age)
        })
    }else if(arr.females){
        arr.females.forEach(function(female){
            console.log(female.name, female.age)
        })
    }

})

//22 mike 21
//22 robert 19
//26 jenny 24
//26 olga 29
```

```javascript
var hotel  = [
{
    rooms:[
    { expensive:[ 'deluxe', 'grand deluxe'] },
    { midPriced:['standard','superior']},
    { economic:['dormitory 6 beds','dormitory 12 beds']}
    ]
}

]
hotel.forEach(function(arr){
    arr.rooms.forEach(function(room){
        if(room.expensive){   
            room.expensive.forEach(function(ele){
                console.log('expensive',ele)
            })
        }else if(room.midPriced){
            room.midPriced.forEach(function(item){
                console.log('midPriced',item)
            })
        }else if(room.economic){
            room.economic.forEach(function(el){
                console.log('economic',el)
            })
        }
    })
})
// expensive deluxe
// expensive grand deluxe
// midPriced standard
// midPriced superior
// economic dormitory 6 beds
// economic dormitory 12 beds
```

And here is the solution to do the same without knowing ANY key in our data structure:

```javascript
hotel.forEach( ele => {
  for( var key in ele ){
   ele[key].forEach( ele2 => {
    for( var key2 in ele2 ){
        ele2[key2].forEach( ele3 => {
            console.log( key2, ele3)
            })
        }
        })
    }
    })
```

## Accessing nested Objects

```javascript
var main = {

    males:{
        anto:{
            name:'antonello',
            lastname:'sanna'
        },
        miky:{
            name:'mike',
            lastname:'peterson' 
        }
    },

    females:{
        guenda:{
            name:'guendalina',
            lastname:'juarez'
        },
        jenny:{
            name:'jennifer',
            lastname:'parker'
        }
    }

}
var checkObj = (main)=>{
    if(main.males){
        for(var key in main.males){
            console.log(main.males[key].name,main.males[key].lastname)
        }

    }if(main.females){
        for(var key in main.females){
            console.log(main.females[key].name, main.females[key].lastname)
        }

    }
}
checkObj(main)
                //antonello sanna
                //mike peterson
                //guendalina juarez
                //jennifer parker
```

## Destructuring in a loop

If we are looping on the array of objects or nested arrays it might be handy to do destructuring in the loop declaration rather than access the items of nested elements in the body of the loop.

Consider following examples:

```javascript
let people = [{
  name: 'John',
  age: 20
},{
  name: 'Anna',
  age: 30
},{
  name: 'Laura',
  age: 40
}]

// without destructuring, each element of an array is an object and we are 
// accessing value in the body of the loop with person.name, person.age
people.forEach( (person) => console.log(person.name, person.age))
// John 20
// Anna 30
// Laura 40

// by destructuring object in the loop declaration in the body of the loop 
// we can access values directly with name, age without reference to the object
people.forEach( ({name,age}) => console.log(name, age))
// John 20
// Anna 30
// Laura 40
```
We can do the same for nested arrays:
```javascript
let people = [ ['John', 20],['Anna', 30],['Laura', 40] ]

// with no destructuring we will need to use indexes to access items in each array
people.forEach( (person) => console.log(person[0], person[1]) )
// John 20
// Anna 30
// Laura 40

// with destructuring we have much cleaner code
people.forEach( ([name,age]) => console.log(name, age) )
// John 20
// Anna 30
// Laura 40
```



## Objects containing functions

We can group a set of functionality inside an object by assigning functions to the object keys and then accessing them via object syntax:

```javascript
let calc =  {

  sum: function(num,num2){
      return num+num2;
  },
  subtract: function(num,num2) {
      return num-num2;
  },
  multiply: function(num,num2) {
      return num*num2;
  },
  divide: function(num,num2) {
      return num/num2;
  }
}

calc.divide(10,20)
// ==> 0.5
```

### Passing by Reference or by Value
Since it is not wise to copy object (which can have undefined size), the arguments of functions point to the same object as the one assigned at execution. For numbers and strings, instead, a new copy of that value will be created in the local scope of the function; inaccessible to the original variable.

```javascript
var myObject = {b: 2}
var addProperty = function (obj){
    obj.a = 1
    // or
    obj["a"] = 1
};
addProperty(myObject)
myObject // {b: 2, a: 1}// myObject is modified because in the memory it has the same allocation inside and outside the function


//this one doesn't change the myNumber because its a number (or string) in the global scope
var myNumber = 1
var add1 = function (number){
    number = number + 1
    console.log(number) // it does increase INSIDE the function
    return number
};
add1(myNumber)
myNumber // 1
```

It means we can use dot notation!
Since functions are special types of objects, which can be executed, we can assign properties to them, just like we did with good old objects.

```javascript
var print = function (text) {
    console.log(text)
}
print("hello class")

print.hello = function(){
    console.log("hello")
}
print.hello()

print.bye = function(){
    console.log("bye")
}
print.bye()

print.text = "bye"
print.text // "bye"
```

## `new` as in new object

Sometimes it is useful to have effective ways to create new objects on demand; to do so we use the keyword `new` with a “constructor” function.
the constructor function creates a template object, with a set of properties and/or methods that we can reuse multiple times.

### ES5

```javascript
var NewObjCreator = function (first, last){
    this.firstname = first
    this.lastname = last
    this.tellFullName = function () { return `${this.firstname}, ${this.lastname}` }
}

var mylist = new NewObjCreator("Antonello", "Sanna")

mylist.tellFullName()
// Antonello Sanna
```

### ES6
With ES6 among other useful features we have the addition of classes, although in reality they are just a nicer way to use the constructor functions, they are nonetheless worth knowing and more user-friendly to use.

Below is an example using an ES6 class that is equivalent to the example above using a constructor function.


```javascript
class NewObjCreator {
    constructor(first, last ) {
        this.firstname = first
        this.lastname = last
    }
    tellFullName() {
        return `${this.firstname}, ${this.lastname}`
    }
} 
var mylist = new NewObjCreator("Antonello", "Sanna")

mylist.tellFullName()
// Antonello Sanna
```

Let's create another example, a basic calculator using ES6 classes;

```javascript
class Calculator  {
   constructor(initial = 0){
      this.total = initial;
  }
  add(num){
      this.total += num;
  }
  subtract(num) {
      this.total -= num;
  }
  multiply(num) {
      this.total *= num;
  }
  divide(num) {
      this.total /= num;
  }
  getTotal () {
      return this.total;
  }
}
```

# Prototype

All JavaScript objects inherit properties and methods from a prototype.
For instance the Array that we have all been using so far inherits all its methods from the Array prototype.

When you write [].forEach for example, you are getting this method from the Array's prototype.

You can think of the prototype as of a shared object that all instances of it's class have access to. You declare the methods once in the prototype and then can then use them in all instances of this class.

In case we are defining a class that we will be reusing multiple times throughout our code we can use the power of JavaScript Prototype to avoid repetition.

For instance think of the Array class, the array has tons of methods, and every time we declare a new array, we are creating a new instance of the Array class, and if the methods weren't attached to the prototype we would be creating a copy of these methods every single time we declare an array.

Let's revisit the calculator example only this time we won't declare our method the same way, this time we will add the method to the prototype of our class. This way our method will be declared only once, yet they will be available in all our instances.

```javascript
Calculator.prototype.add      = function (num) { this.total += num }
Calculator.prototype.subtract = function (num) {this.total -= num;}
Calculator.prototype.multiply = function (num) {this.total *= num;}
Calculator.prototype.getTotal = function() { return this.total }
```

## Adding custom methods to JavaScript internals

It is possible to add your own custom methods to the JavaScript internals which will work in the scope of your app. For example, you are working on the app there you need to clear objects often. The best solution would be to write a function for that and make it available for the entire app. But since we are talking about prototypes we can also do that:

```javascript
// assigning a custom method "clear" to the object prototype
Object.prototype.clear = function(){
var props = Object.getOwnPropertyNames(this);
for (var i = 0; i < props.length; i++) {
  delete this[props[i]];
}
}
// now if we will initialize a new object
let foo = {a:1,b:2}
// we can use our custom method to clear it:
foo.clear()
// our foo object would be empty
console.log(foo)
//> {}
```

> Why adding custom methods to the JS internals is not recommended? One of the reasons -- imagine, your app is deployed in production and new version of JS specification is released where `.clear` is a new built-in method doing something (you will be lucky if it will do exactly the same thing)...

## Extends 

We can extend an existing class and borrow all its methods and add more to it using the keyword extends.
This way we leave our original class untouched.

```javascript
class CoolerCalc extends Calculator {
    isEven(num) {
      return num % 2 ===0;
  }
}

var coolCalc = new CoolerCalc()
// this instance will have all methods from Calculator plus the new one we added.
```

## Extends with initial parameters:

```javascript

class Calculator  {
   constructor(initial = 0){
      this.total = initial;
  }
  add(num){
      this.total += num;
  }
  subtract(num) {
      this.total -= num;
  }
  multiply(num) {
      this.total *= num;
  }
  divide(num) {
      this.total /= num;
  }
  getTotal () {
      return this.total;
  }
}

// if we want to pass initial values into extended class instance we also need to use super and pass arguments from the main class
class CoolerCalc extends Calculator {
    constructor(initial, secondarg){
        super(initial)
        this.secondNumber = secondarg
    }
    isEven(num) {
      return num % 2 ===0;
    }
}


var coolercalc = new CoolerCalc(10,50)

coolercalc
// CoolerCalc {total: 10, secondNumber: 50}

```

> Composition vs Inheritance in plain English: https://javascript.plainenglish.io/inheritance-is-a-vs-composition-has-a-in-javascript-98fb96dfa0e6


# Exercise time!
