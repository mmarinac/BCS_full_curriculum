# Express middlewares

Middleware functions are functions that have access to the request object (req), the response object (res), 
and the next function in the application’s request-response cycle. The next function is a function in the Express router which, when invoked, executes the middleware succeeding the current middleware.
Middleware functions are often used as a mechanism to verify access levels before entering a route, 
error handling, data validation, etc.

# Handling Errors in Express

Handling error is a crucial part while building web apps, fortunately Express gives you a nice way to handle your errors with some default functions.

Errors returned from synchronous functions : 

```javascript
app.get('/', function (req, res) {
  throw new Error('Something went wrong') // Express will catch this on its own.
})
```

Errors returned from asynchronous functions, should be passed to the next() function,
in the next example both server and client will receive a default error with status code 500
(server in the terminal and client in the browser console):

```javascript
app.get('/', function (req, res, next) {
  fs.readFile('/file-does-not-exist', function (err, data) {
    if (err) {
      next(err) // Pass errors to Express.
    } else {
      res.send(data)
    }
  })
})
```

We can also be more specific and assign a status code and a message to the error:

```javascript
app.get('/', function (req, res, next) {
  fs.readFile('/file-does-not-exist', function (err, data) {
    if (err) {
      err.statusCode = 403
      err.message = '❌  There is some error in your server ❌ '
      next(err) // Pass errors to Express.
    } else {
      res.send(data)
    }
  })
})
```

or

```javascript
app.get('/', function (req, res, next) {
  fs.readFile('/file-does-not-exist', function (err, data) {
    if (err) {
       next(createError(401, '❌  There is some error in your server ❌ '))// Pass errors to Express.
    } else {
      res.send(data)
    }
  })
})
```

If internal server errors happens could be useful for the mainteiners to receive a notification 
through email or slack, like in the following example:

```javascript
const fetch = require("node-fetch");

const send_message = async(next) => {
      await fetch(`https://hooks.slack.com/services/${your_token_here}`, {
        body :JSON.stringify({text:'❌  There is some error in your server ❌ '}),
        headers : {"Content-Type": "application/json"},
        method: "POST"
      })
      next(createError('❌  There is some error in your server ❌ '))
}

app.get('/',async (req,res,next) => {
  try{
      //The variable name doesn't exist
      console.log(name)
  }catch(error){
      send_message(next)
  }
})
```