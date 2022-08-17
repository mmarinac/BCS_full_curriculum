# Basic functions

---

<details>
    <summary>🎬 Video: JS -- intro to functions</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/3-Wi2p3a5V4?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---

Functions are a way for us to minimise repetition in our code.
We use them to execute the same piece of code multiple times without rewriting it.

In this  chapter we are going to use functions at their most basic level.

Let’s see a very basic example of a function:


    var sayHello = () => {
        console.log('Hello world!')
    }
    
Here we have defined a function called sayHello that when executed will print out the phrase Hello world!. This is known as function declaration, we defined the function and now it can be used or called.

Keep in mind that the code inside it will not be executed until the function is called.

In order to call our function we need to write the name of the function followed by parentheses.

    sayHello()
    
Here we are executing, or calling our function.



## Arguments

Functions can take arguments, arguments are data that comes from outside the function and can be used inside it.


    var saySomething = (something) => {
    // here we are waiting for one argument
    // its value will be anything that we pass to it when we call the function.
      console.log(something)
    }
    
    saySomething('Hello')
    // the value of our argument something is now Hello
    
    saySomething(2+2)
    // the value of our argument something is now 4


You can pass as many arguments as you like to your function, let’s see an example where we create a super basic calculator that only adds to numbers.


    var calculator = (a, b) => {
      console.log(a + b);
    } 
    
    calculator(10, 5)
    //this function logs 15

> When function can take more than one argument it might be a good idea to declare them as an object and during a function call pass data inside an object where we can explicitely assign data to specific arguments, compare this two examples:

```javascript
let greeting =(username, age, city)=> console.log('Hello ' + username + ', you are ' + age + ' years old and you live in ' + city)
greeting('Mike',30,'Barcelona')
// ==> Hello Mike, you are 30 years old and you live in Barcelona

// but if we will mess up the order of arguments it will be completely unusable output:
greeting(30, 'Barcelona', 'Mike')
// ==> Hello 30, you are Barcelona years old and you live in Mike

// if instead we will declare parameters in the object inside curly brackets
let greeting =({username, age, city})=> console.log('Hello ' + username + ', you are ' + age + ' years old and you live in ' + city)
// and explicitly assign values to the argument in a function call even disregarding the order it will be fine
greeting({age:30, city:'Barcelona', username:'Mike'})
// ==> Hello Mike, you are 30 years old and you live in Barcelona
```

## Default parameters

Default parameters allows you to set default values for your function parameters if no value is passed or if undefined is passed. 

```javascript
    const sum = ( num1 = 10 , num2 = 20 ) => num1 + num2
    sum()
    //30
    
    const sum = ( num1 = 10 , num2 = 20 ) => num1 + num2
    sum(20,50)
    //70
    
    const sum = ( num1 = 10 , num2 = 20 ) => num1 + num2
    sum(80)
    //100
```

## Return

So far all we did was to log the result of our function, but if we do it this way, our functions has no output because it returns nothing.

Let’s see what it means…


    var calculator = (a, b) => {
      console.log(a + b);
    } 
    
    var total = calculator(10, 5)
    // You may expect the value of total to be 15 but instead it will be undefined
    
    console.log('I am total', total)
    //undefined


In order for our function to give us back a value we need to use the  `return`  keyword.


    var calculator = (a, b) => {
      return a + b;
    } 
    var total =  calculator(10 , 5)
    console.log('I am total', total)
    //15


This was a brief intro to functions,  as we are going to see them more in depth in block 5.

