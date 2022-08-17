# React 05: Conditional Rendering

---

<details>
    <summary>🎬 Video: React -- conditional rendering</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/tAuXFp7KO_E?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

[Sample code from the video lesson](https://gitlab.com/gk3000/BCS_JS_BOOTCAMP_FILES_TDD/snippets/1969478)

---

There are several ways to use conditions in the React `render` function; if you are outside the `return` statement you can use a standard `if` statement:

<!-- tabs:start -->
#### **Class components**
```javascript 
import React from 'react' 

export default class CompOne extends React.Component{
  render(){
    this.name = "Mariangel"
    if(this.name == "Stefano"){
      return <h1>Welcome back Stefano!</h1>
    }else {
      return <h1>Hello {this.name} and thanks for joining us!</h1>
    }
  }
}
```

#### **Function components**
```javascript
import React from 'react' 

export default function CompOne () {
  const name = "Mariangel"
  if (name == "Stefano") {
    return <h1>Welcome back Stefano!</h1>
  } else {
    return <h1>Hello {name} and thanks for joining us!</h1>
  }
}
```
<!-- tabs:end -->

In case you need to apply conditional rendering inside the `return` statement you must use the ternary operator.

## Ternary operator in React

As we already know, the ternary operator is a shorter way to write `if` statements:

```js
    condition ? code to run if the condition is met : code to run otherwise
```

Example in pure JS:

```js
var num   = Number(prompt('enter a number'))
var fixed = 10
num > fixed ? document.write(`<h1>${num} us bigger than ${fixed}</h1>`)
: document.write(`<h1>${num} is smaller than ${fixed}</h1>`)
```

same example using if statement

```js
var num   = Number(prompt('enter a number'))
var fixed = 10
if (num > fixed) {
 document.write(`<h1>${num} us bigger than ${fixed}</h1>`)
}else{
 document.write(`<h1>${num} is smaller than ${fixed}</h1>`)
}
```

Now let’s try the ternary operator in React:

<!-- tabs:start -->
#### **Class components**
```javascript
import React from 'react'

export default class CompOne extends React.Component{
  render(){
    this.name = "Lora"
    return( 
      <div>
      { 
        this.name =="Golda" ? <h1>Welcome back Golda!</h1> :
        <h1>Hello {this.name} and thanks for joining us!!!</h1> 
      }
      </div>

      )
  }
}
```

#### **Function components**
```javascript
import React from 'react';

export default function CompOne() {
	const name = 'Lora';
	return (
		<div>
			{name === 'Golda' ? <h1>Welcome back Golda!</h1> : <h1>Hello {name} and thanks for joining us!!!</h1>}∑
		</div>
	);
}
```

<!-- tabs:end -->

<iframe src="https://codesandbox.io/embed/react-block-5-1-6vhb1?fontsize=14" title="React Block 5 - 1" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

If you only want to render something in specific condition and otherwise do nothing you can also use `&&` like this:

<!-- tabs:start -->
#### **Class components**
```javascript
import React from 'react'

export default class CompOne extends React.Component{
  render(){
    this.name = "Lora"
    return( 
      <div>
      { 
        this.name =="Lora" && <h1>Welcome back Golda!</h1>  
      }
      </div>

      )
  }
}
```

#### **Function components**
```javascript
import React from 'react';

export default function CompOne() {
	const name = 'Lora';
	return <div>{name === 'Lora' && <h1>Welcome back Golda!</h1>}</div>;
}
```
<!-- tabs:end -->
And that's pretty much it for the conditionals! 


# Exercise time!