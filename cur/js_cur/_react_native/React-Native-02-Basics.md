# React native 02: Basics

React Native has many components which we can use out of the box, let’s see some of the most commons.

## The View tag

https://reactnative.dev/docs/view

The `View` tag is somehow the equivalent of the `div` in HTML, it is a container to wrap our component (or part of it).

Let’s say that we have one very simple component which does only one thing, says "Hello!".
```javascript
import React from 'react'
import {View, Text} from 'react-native'

export default () =>(
  <View>
      <Text>
          Hello!
      </Text>
  </View>
)
```   

Now all we really care about here is to display the message "Hello!", however the `View` tag itself cannot contain text (text must be wrapped in a Text tag).

Now if we were to leave our component as it is we couldn't still see our text very clearly. In order to do that we need to add in some basic styling.

Let’s start by importing StyleSheet from React Native.

```javascript
import { StyleSheet, Text, View } from 'react-native';
```

Then we can create our style object and apply it to our `View`.
```javascript
export default () =>(
      <View style={styles.container}>
            <Text>Open up App.js to start working on your app!</Text>
      </View>
)

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```
One thing to keep in mind is that certain components can have certain styles attribute, unlike CSS in the DOM where you can apply almost any attribute to any tag and in the worst case scenario it won’t have any effect, if you apply an inappropriate styling to a tag in RN you get a nasty error and the app simply won’t run until you fix it!

Coming from web development background styling in React native could be a bit frustrating at first, however thanks to flexbox and external packages it’s possible to style your application however you like it.

## TextInput tag

https://reactnative.dev/docs/textinput

Whenever we need to get data from the user (for example from a form) we need a `textInput` tag, these are equivalent to an input field in HTML.
```javascript
const [email, setEmail] = useState('')

<TextInput
    style={styles.input}
    onChangeText={(text) => setEmail(text)}
    // here we take the value from our text input and set the state so that we can 
    //access it.
    value={email}
    onSubmitEditing={(event) => setEmail( event.nativeEvent.text)}
    // to submit on press key Enter
/>

const styles = StyleSheet.create({
  input:{
    height: 40, 
    //40px height to our input
    width:100,
    //100px width
    borderColor: 'black', 
    //color of our border
    borderWidth: 1
    //width of our border
  }
});
```
Let’s now use our three components and make a very basic app which will write `onChange` the text that we add in our `TextInput`.

```javascript
import React from 'react';
import { StyleSheet, Text, View, Button, TextInput } from 'react-native';

export default function App() {
  const [text, setText] = useState('')

  return (
      <View style={styles.container}>
          <Text style={styles.text}>{text}</Text>
          <TextInput
            style={styles.input}
            onChangeText={(text) => setText(text)}
          />
      </View>
  )
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  input:{
    height: 40, 
    borderColor: 'gray', 
    width:100,
    borderWidth: 1  
  },
  text:{
    fontSize:35,
    color:'red'
  }
});
```
    
## Button tag

https://reactnative.dev/docs/button

The `button` tag is the equivalent of an HTML `button`. `Button` tag expects certain props in order to work.
the required props are `onPress` function and the `title`. The `onPress` function is the equivalent of the `onClick` event handler in Reactjs. `Title` is just a string used for label, however it is required.

So let’s see a basics example of a RN Button.
```javascript
<Button
    onPress={myAmazingFunction}
    title="Press me"
    color="#841584"
/>
```
Now let’s insert this button to our application and make it clear our state when clicked!

Let’s add this to our code:
```javascript
const clearMyInputPlease = () => setText('')

//======in the render function ======
<Button
  onPress={clearMyInputPlease}
  title="Clear state.text"
  color="#841584"
/>
```

# ToDo App

Now let’s create a simple ToDo app using only these 4 components that we just learned.

---

<details>
    <summary>🎬 Video: React Native -- ToDo App</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/_0JpYKXrqJI?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

## Version 1

We can add todos, and clear the input field.

```javascript
import React, {useState} from 'react';
import { StyleSheet, Text, View, Button, TextInput } from 'react-native';

export default function App() {
  const [text, setText] = useState('')
  const [todos, setTodos] = useState([])

  const addToList = () =>{
      const temp = [...todos] 
      temp.push(text)
      setTodos([...temp])
      setText('')
  }
  const showTodos = () => (
    todos.map((todo, i)=>(
        <Text 
            style={styles.text}
            key={i}>{todo}
        </Text>
    ))
  )

  return (
    <View style={styles.container}>
        <TextInput
            style={styles.input}
            onChangeText={(text) => setText(text)}
            value={text}
        />
        <Button
            onPress={addToList}
            title="Add Todo!"
            color="#841584"
        />
        {showTodos()}
    </View>
  )
}

const styles = StyleSheet.create({
  container: {
    // flex: 1,
    top:20,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  input:{
    height: 40, 
    borderColor: 'gray', 
    width:100,
    borderWidth: 1  
  },
  text:{
    fontSize:35,
    color:'red'
  }
});
```

## Version 2

Now let’s add the possibility of removing todos.
```javascript
import React, {useState} from 'react';
import { StyleSheet, Text, View, Button, TextInput } from 'react-native';

export default function App() {
  const [text, setText] = useState('')
  const [todos, setTodos] = useState([])

  const addToList = () =>{
      const temp = [...todos] 
      temp.push(text)
      setTodos([...temp])
      setText('')
  }

  const removeTodo = (idx) => {
      const temp = [...todos]
      temp.splice(idx, 1)
      setTodos([...temp])
  }

  const showTodos = () => (
      todos.map((todo, idx)=>{
        let bgc;
        idx % 2 !=0 ? bgc = "#ddd" : bgc = 'transparent'
        return <View 
                  key={idx} 
                  style={{backgroundColor:bgc}}>
                <View style={styles.box}>
                    <Text
                      numberOfLines={1} 
                      style={styles.text} >{todo}
                    </Text>
                    <Button
                        onPress={( ) => removeTodo(idx)}
                        title="X"
                        color="red"
                    />
                 </View>
                 <View
                    style={{
                      borderBottomColor: 'black',
                      borderBottomWidth: 1,
                      width:300
                    }}
                  />
              </View>
        })
  )
  return (
        <View style={styles.container}>
            <View style= {styles.box}>
                <TextInput
                    style={styles.input}
                    onChangeText={(text) => setText(text)}
                    value={text}
                />
                <View style ={styles.button}>
                    <Button
                        onPress={addToList}
                        title="+"
                        color="green"
                />
                </View>
            </View>
              {showTodos()}
        </View>
  )
}

const styles = StyleSheet.create({
  container: {
    // flex: 1,
    top:30,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  input:{
    height: 40, 
    borderColor: 'gray', 
    width:150,
    borderWidth: 1  
  },
  text:{
    fontSize:20,
    color:'green'
  },
  button:{
    borderColor:'black',
    borderWidth:1,
    height:40,
    width:150
  },
  box:{
    flexDirection:'row',
    width:'80%',
    justifyContent:'center',
    alignItems:'center'
  }
});
```    

You can also try this code here…
https://snack.expo.io/@gk3000/suspicious-apples

## Image tag

https://reactnative.dev/docs/image

Image tag is similar to the HTML `img` and as you would expect they are used to display images. If your images are loaded from a URL, you will need to give it a width and a height.

> Remember to import Image from react-native first!
```javascript
<Image
  style={{
    width: 60, 
    height: 60, 
  }}
  source={{
    uri: 'YOUR_IMAGE_URL'
  }}
/>
```
As you can see from the official page linked above we aren’t limited to use URL’s for our pictures, we can also have locally saved images. Also to notice that for local images giving dimensions isn’t mandatory.

```javascript
<Image
  source={require('./photos/myImage.png')}
/>
```
Let’s add this image to our ToDo app as the first thing inside our View tag.
```javascript
<Image
    style={{
      minWidth: 60, 
      minHeight: 60, 
      marginBottom:10,
    }}
  source={{
  uri: 'https://sdtimes.com/wp-content/uploads/2014/09/todo-manager-icon.png'}}
/>
```
# Example Snippets
### Flexbox Layout example using react native with a top, a mid and a bottom section
```javascript
// App.js
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';
import Navbar from './NavBar';
import MidSection from './MidSection';
import Footer from './Footer';

export default function App() {
    return (
      <View style={styles.container}>
          <Navbar/>
          <MidSection/>
          <Footer/>
      </View>
    );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```

```javascript
// NavBar.js
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

export default () => <View>
                        <Text>I am the Navbar :)</Text>
                     </View>
```

```javascript
// MidSection.js
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

export default () => <View>
                        <Text>I am the Mid section</Text>
                     </View>
```

```javascript
// Footer.js
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

export default () => <View>
                        <Text>I am the Footer</Text>
                     </View>
```
## Challenge

Add persistence data to the ToDo App so that the todos are permanently saved in the phone’s memory.
We are going to use R.N AsyncStorage that is the equivalent of the localStorage and also use the same methods.

### You will need to use this:

https://www.npmjs.com/package/@react-native-async-storage/async-storage

If our app need to persist data but we don't have a server, we can use the local memory of the phone.

In order to be able to use the AsyncStorage it has to be installed.

```
npm install @react-native-async-storage/async-storage
```

Remember to import the AsyncStorage at the top of your file

```javascript
import AsyncStorage from '@react-native-async-storage/async-storage';
```

Persisting data is similar to the `localStorage` of the browser only in this case it doesn't depend on the browser but uses the phone's memory. In the same way we need to stringify data before adding to asyncStorage (if it is not already a string):
```javascript
// some data
const [data, setData]=useState([1,2,3,4,5])

const _storeData = async () => {
  try {
    // we need to stringify our array into a string
    await AsyncStorage.setItem('dataNumbers', JSON.stringify(data) );
  } catch (error) {
    // Error saving data
  }
};

const _retrieveData = async () => {
  try {
    const value = await AsyncStorage.getItem('dataNumbers');
    let bringBackToArray= JSON.parse(value)
// now we have data restored from asyncStorage parsed back into an array which we can use
} catch (error) {
    // Error retrieving data
  }
};
```