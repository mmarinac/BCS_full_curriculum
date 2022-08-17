# React Native 01: Setup/Intro

> React Native official documentation: https://reactnative.dev

---

<details>
    <summary>🎬 Video: React Native -- intro</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/RUaWhwbJ7pQ?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

Getting started with: https://facebook.github.io/react-native/docs/0.60/getting-started

API reference: https://facebook.github.io/react-native/docs/0.60/activityindicator

With React Native, you don't build a "mobile web app", an "HTML5 app", or a "hybrid app". You build a real mobile app that's indistinguishable from an app built using Objective-C or Java. React Native uses the same fundamental UI building blocks as regular iOS and Android apps. You just put those building blocks together using JavaScript and React.

*from https://facebook.github.io/react-native/*

The syntax is for the most part like in React.js there are however some differences, most of which are inside the render function.

To begin with there is no DOM!

In React Native there are only React Native tags, so no `div`, `ul`, `h1`... none of them are available.

Let’s see an example of Hello World in RN.


```javascript
import React from 'react'
import {Text, View, StyleSheet }  from 'react-native';

// The Text tag is where we write our text
// The View tag is our container, is sort of the div tag in the DOM.
// The StyleSheet tag is an object that we use to write the styles for our component.

export default ()=>(
  <View style ={styles.container}>
    <Text style={styles.text}>
      Hello World!
    </Text>
  </View>
)
const styles = StyleSheet.create({
  container: {
    flex: 1,
    top:50,
    backgroundColor: '#fff',
    alignItems: 'center',
  },
  text:{
    fontSize:20
  }
});
```
    

To get started with React Native we need to set up some development environment. 

One of the easiest and fastest ways to begin coding is called [Snack](https://snack.expo.io) and essentially it is online IDE with code editor and emulator built-in. The only downside is that it doesn't have debugger. 

Another way would be to install Expo, which will give us an online IDE to work with along with cross-platform components and we can our mobile phones to display the app (plus, it has a debugger).


Then let’s install the command line by running:

    npm install expo-cli --global

> As always with installing some package globally on Mac you might need to run it with `sudo` command before and when prompted type your laptop user's password: `sudo npm install expo-cli --global`

Now that we have our environment set up and we ready to start writing some code!
 
Open the terminal and let's create our first React-native project by running:

    expo init myfirstapp

It will create a new empty project with name 'myfirstapp', of course you can name you app anything else, it doesn't have to be 'myfirstapp'

> Windows users: if terminal is complaining about not being able to run expo in interactive mode start *powershell* as administrator and run the same command from there. To run powershell as administrator right-click on the powershell icon and select 'Run as administrator'. Then in the PowerShell run `Set-ExecutionPolicy RemoteSigned` and confirm with "yes". After that `expo init nameofyourproject` should work.

In the terminal go into the folder of the project you just created wuth `cd myfirstapp` and run `expo start`

Expo will generate a react native app with some default text to get you started. You can see that either by running it in the IOS / Android emulator or by running it in your device. To run it in your device you will also need to install the Expo client app in it.

[Download for Android from the Play Store](https://play.google.com/store/apps/details?id=host.exp.exponent) or [for iOS from the App Store](https://itunes.com/apps/exponent).

After you started the app you will see a QR code in the browser to scan and open your project in Expo mobile client on your phone.

Let’s open the project that expo generated for us and start changing the text inside the Text tag <Text> inside the App.js file.

You will see that as soon as you make any changes to this file expo will re-compile the JavaScript bundle (your app!) and will automatically update itself.

