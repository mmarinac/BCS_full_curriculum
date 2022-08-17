## Closure

---

<details>
    <summary>🎬 Video: closures, recursion</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/hOnLq-GQQqE?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---



A **closure** is an inner function that has access to the outer (enclosing) function's variables—scope chain. The **closure** has three scope chains: it has access to its own scope (variables **defined** between its curly brackets), it has access to the outer function's variables, and it has access to the global variables.

*A closure only exists when an inner function makes use of a variable defined from an outer function that has returned.*

If it doesn't make use of any variables then is a nested function.

In the examples below we see that the inner function has access to both the argument passed to the outer function and the variable declared within it.

```javascript
function main (num) {
    var insideNum = 3
    function innerFun() { 
        console.log(num * insideNum) 
    }
        return innerFun()
}
```

Or a shorthand version of the same where the inner function is anonymous and executed immediately.

```javascript
function main (num) {
    var insideNum = 3
    return function () { 
        console.log(num * insideNum) 
    }()
}
```

Within the closure the inner function has access to all variables declared inside the scope of the outer function.

This is an example where the function is declared outside and yet has access to the variable.

```javascript
var outer = function () {
        var inner = function(){        
          console.log( outerVariable )
        } //inner function declaration ends here.
        var outerVariable = "Hello closure"
        return inner()
}
```

Let’s see a more convoluted example that just confirms our point. The below example is just to show that no matter how many level is nested you can still have access to the variable declared in the outer function.

```javascript
var grandfather = () => {
        var favDrink = "red wine"
        return function () {
                var like = "Grandfather "
                return function (){
                        var fav = "favorite drink is "
                        return function (){
                                console.log(like + fav + favDrink)
                        }()
                }()
        }()

}
grandfather()
//Grandfather favorite drink is red wine
```

In closures the function **remembers only the variables that have been used  within the inner function**.

```javascript
var outer = function () {
var data = "something"
var fact = "remember"
        return function () {
                debugger
                return data
        }()
}
outer()
// trying accessing the variables form within the debugger we get:
data
//"something"
fact
//Uncaught ReferenceError: fact is not defined
    at eval (eval at <anonymous> (:5:3), <anonymous>:1:1)
    at <anonymous>:5:3
    at outer (<anonymous>:7:3)
    at <anonymous>:1:1
(anonymous) @ VM715:1
(anonymous) @ VM705:5
outer @ VM705:7
(anonymous) @ VM707:1
```

But what use do we have for closure?

Well we can use closure to define private variables. Using closure each function will have access to its own copy of the variable not modifying the original.

Let’s check the below example.

```javascript
var counter = () =>{
    var count = 0;
    return function inner (){
        count++;
        return count
    }
}
counter()
//ƒ inner(){
  //count++;
  //return count
// }
var x= counter()
x()
//1
//Here we get one as expected
x()
//2
//Here we modified count to be 2
var y = counter()
y()
//1
//However when we check the value of count from our new function y we get one and not 2 because the original count is not being modified by our function x.
```