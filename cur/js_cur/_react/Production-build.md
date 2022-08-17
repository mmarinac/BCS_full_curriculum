# Building your create-react-app for production and serving with Express

## Set up a basic server to serve your app:

In your repository, create a file called server.js:
	
	touch server.js

In `server.js`, copy/paste the following code:

```js
//server.js
const express = require('express');

// comment the next line out if you don't want favicon
// const favicon = require('express-favicon'); 
// if you want to have a favicon
// favicon.ico goes to /public folder to replace the original one from React

const path = require('path');
const port = process.env.PORT || 8080;
const app = express();

//comment this out if you don't use favicon
// app.use(favicon(__dirname + '/build/favicon.ico'));


// the __dirname is the current directory from where the script is running
app.use(express.static(__dirname));
app.use(express.static(path.join(__dirname, 'build')));

app.get('/*', function (req, res) {
  res.sendFile(path.join(__dirname, 'build', 'index.html'));
});
app.listen(port);
```

Install `express-favicon` package if you do not have it yet. 

This code creates a special Node JS server that can serve minified/uglified JS. 

Make sure you add express, express-favicon, and path to your dependencies:

	npm install --save express express-favicon path 

In your package.json file, change the start script to the following:

	start: "node server.js"

## Create a React production build:

To create your production build, run the following in your terminal:

	npm run build

or

	yarn build 

Your build will be stored in the generated `build` folder.

Then add the following to your .gitignore file:


	src/*
	public/*
	build/static/css/*.map
	build/static/js/*.map

.gitignoring these files means that only your minified JS and CSS will be published to the source folder which anyone can view using the developer tools.

>IMPORTANT: Remove the following line from your .gitignore file:
	/build 

## Start your app:

	node server.js
	
> You can also add script to package.json, such as "prodstart": "node server.js"

The app will start and run on the port, specified in the `server.js` file