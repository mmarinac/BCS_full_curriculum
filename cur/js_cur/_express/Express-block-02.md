# Express block 02

---

<details>
    <summary>🎬 Video: Express - passing data via body</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/qVlzwp-WHFk?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

Sample code from the video lesson:

<iframe height="400px" width="100%" src="https://repl.it/@gk3000/express-passing-data-via-body?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

---


## Express Routing

**How to send more data to the server**
HTTP request types

----------

In order to allow the user to communicate with the server, a verb has been added to the HTTP request, also called Method. There are 2 main types of methods: POST and GET.

----------

Commonly GET request are used to get data and POST are used to send data to the server.

> GET http://www.google.com/home/welcome?name=gk&age=100
----------

GET vs POST

GET

- The data is in the URL: /test/:name/:location
- GET requests remain in the browser history
- GET requests can be bookmarked
- GET requests should never be used when dealing with sensitive data
- GET requests have length restrictions
- GET requests are more appropriate to retrieve data
----------

POST

- Data is send in the message body. WE CAN SEND MORE DATA!
- POST requests are never cached
- POST requests do not remain in the browser history
- POST requests cannot be bookmarked
- POST requests have no restrictions on data length
- POST requests are more appropriate to store data
----------

[MDN reference for HTTP requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

----------
## Express Routing

We use HTTP - HyperText Transfer Protocol - a series of rules that is used to transfer information between servers and browsers.

One route per function
    
    const express = require('express')
    const app = express()
    
    app.use('/hello!', (req, res)=> {
        res.send('Hello World!')
    })
    
    app.use('/bye!', (req, res)=> {
        res.send('Bye World')
    })
    
    app.listen(3000,  ()=> {
        console.log('listening on port 3000!')
    })

If the incoming route matches one of the declared then callback app.method in it will be triggered!


## Parameters

Express has built-in methods to read the url. The most common ones are parameters, 
where part of the url will be accessible to the user in the `req.params`object, 
and query values, which can be accessed from the `req.query` object.

    app.use('/user/:name/:age',  (req, res)=> {
        res.send('Hello ' + req.params.name + '. Your age is: '+ req.params.age)
    })


    app.use('/user/info',  (req, res)=> {
        //to pass data with query use this syntax:
        // question mark, key name, equal sign, value, such as:
        // your_domain_name/user/info?name=gk&age=100

        req.originalUrl // allows you to grab the url from the request
        // in this case it would be /user/info?name=gk&age=100

        // eventually we can send back the name and age from the request
        res.send('Hello ' + req.query.name + '. Your age is: '+ req.query.age)
    })


## Static Content

Static/public assets (.js, css & others) files can be made accessible through the following middleware. In this case all paths that start with '/assets' (any path prefix can be used) will be considered as assets and will be served by files located under a file in the project’s root dir, in a folder called `static`.

What you need to do is add this into your main server file:

```javascript
app.use('/assets', express.static(__dirname + '/static'))
```

where 'static' is the name of the folder in your server with static files and 'assets' is the virtual path for the users to navigate to to fetch stuff. So if you have an image banana.jpg inside 'static' folder in the root of your express app the path to use it would be domainname.com/assets/banana.jpg.

# Sending data in the body

To send data in the body of POST requests and get it in the server we need to configure express:

```javascript
const express = require('express')
const app = express()

app.use(express.urlencoded({extended:true}))
app.use(express.json())
```

> For version of express prior to 4.16.0 we need to install body-parser and use it instead:

> Example of using body parser

    We first need to install body-parser package from the terminal
    in the folder of a project with this line of code:
    
    npm i body-parser

> And then add this into your main express file:
    
    // require and run express in a single line
    const app=require('express')()
    // add body parser
    const bodyParser= require('body-parser')
    app.use(bodyParser.urlencoded({extended: true}))
    app.use(bodyParser.json())
    
    // Now we have access to the body through the req.body object
    app.post('/hello', function (req, res) {
    res.send('Hello ' + req.body.name + '. Your age is: '+ req.body.age)
    })
    
    app.listen(3000,()=>{console.log('yeahhh')})




# PUT & DELETE

The PUT method can be used to **to replace** an existing one, like using the POST method,
the request has body object. 

The PATCH method can be used to **to update** an existing one, it also allows to send the body object.

The DELETE method is used **to remove** a specific resource; although the body object could be used, it is unusual to use it in this kind of requests.

# HTTP status codes

When the client makes a request to the server, it respond whit a HTTP status code that allows us to understand what is happening in the server and fix errors in case.

HTTP status code are divided in 5 categories:

- Informational responses (100–199)
- Successful responses (200–299)
- Redirects (300–399)
- Client errors (400–499)
- Server errors (500–599)

Even if we don't need to know all of them, it is important to know the most useful ones:

##### 2**  Successful responses


**200 -    OK     -** The exchange between the client and the server is complete. Everything is set up properly and                             nothing should negatively impact.
                      

**201 - CREATED   -** Like status code 200, means that the request was successful, but it also resulted in a new                                resource being created. This is typically the response sent after POST requests, or some PUT                              requests.
 
**202 - ACCEPTED  -** The client requested to create something on the server.The request has been accepted for                                  processing, but the processing has not been completed.

##### 4**  Client errors    

**400 - BAD REQUEST  -** The server could not understand the request due to invalid syntax.

**401 - UNAUTHORIZED -** Indicates that the request has not been applied because it lacks valid authentication                                     credentials for the target resource.

**403 - FORBIDDEN    -** The client does not have access rights to the content. Unlike 401, the client's identity is                               known to the server.

**404 - NOT FOUND    -** The resource no longer exists, and the server cannot return any information. A 404 status code                            does not indicate whether the resource is temporarily or permanently missing. But if a resource                           is permanently removed, a 410 (Gone) should be used instead of a 404 status.

**409 - CONFLICT     -** The server thinks that the request submitted by the client can not be completed because it                                conflicts with some rule already established. 

##### 5**  Server errors   

**500 - INTERNAL SERVER ERROR  -** The server cannot process the request for an unknown reason.

**501 - NOT IMPLEMENTED        -** The server either does not recognize the request method, or it cannot support the                                         request.

**502 - BAD GATEWAY            -** The 502 status code, or Bad Gateway error, means that the server is a gateway or proxy                                    server, and it is not receiving a valid response from the backend servers that should                                     actually fulfill the request.

###### To include status codes in the HTTP response, we can use the following syntax:

      response.status(200).send({ok:true, data: somedata})

### Postman

Since we can only test GET requests in the browser and can't send data in the body of the request, we are going to use Postman from now on to build/test back-end APIs. You can install it from [getpostman.com](https://www.postman.com).

Please check those resources to learn more about Postman:

[Video tutorials](https://www.getpostman.com/resources/videos-tutorials/)

[Learning center](https://learning.getpostman.com)

## **TODO APP EXAMPLE:**

https://gitlab.com/barcelonacodeschool/todo_app_express_step_by_step
