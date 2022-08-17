# Express block 04: EJS / LEGACY

Though we are not going to use EJS throughout the course this text could show you how easy it is to pass date between frontend and your server.

# Express & EJS & public
## EJS

EJS (embedded JavaScript) is a templating engine which allows you to edit HTML (ideally any text file should work) using javascript. Anything within the`<%=...%>` tags will be evaluated as JavaScript and then replaced in the file according to the tags indication
This code inside an .ejs file

    <% var title = "BCS students are awesome" %>
    <h1> title: <%= title %> </h1>

Will become

    BCS students are awesome
    <h1> title: BCS students are awesome </h1>

## EJS tags

There are 3 main types of tags in ejs
With the equal sign

    <%= "BCS students are awesome" %> // adds "BCS students are awesome" to the text

With no equal sign

    <% "BCS students are awesome" %> // adds nothing to the text

With the dash

    <%- "BCS students are awesome" -%> // used to render html like characters!

Example

> File.ejs
    <ul>
    <% numbers = [1,6,4,7,3] %>
    <% for(var i=0; i<numbers.length; i++) {%>
    <% if (numbers[i]>5) { %>
    <li><%= numbers[i] %></li>
    <% } else { %>
    <li><%= "banana" %></li>
    <% } %>
    <% } %>
    </ul>

Will output

> File.html
    <ul>
    <li>banana</li>
    <li>6</li>
    <li>banana</li>
    <li>7</li>
    <li>banana</li>
    </ul>

## Express & EJS

**Integrating EJS with Express**
Integrating Express with ejs is relatively easy, we only need to add a few lines to our app. But first don’t forget to add EJS package to your project.

    > npm install ejs --save
    
    app.set('view engine', 'ejs')
    app.set('view cache', false);

We can now use EJS templates through the `res.render` method that will look for a file called “rootToMyApp/views/hello.ejs” in a folder called views in the root directory of your app.

    app.get("/hello", function (req, res) {
    res.render("hello", { sentence: "hello", to: "you" })
    })

Now these variables `sentence` and `to` will be defined within your template.
Example

    app.get("/hello", function (req, res) {
    res.render("hello", { sentence: "hello", to: "you" })
    })
> hello.ejs
    <div>
    <span><%= sentence %></span>
    <span><%= to %>!!!</span>
    </div>

Will output

> hello.html
    <div>
    <span>hello</span>
    <span>you!!!</span>
    </div>

## Sublime & EJS

Install 2 packages:
SublimeERB & EJS2
If you have package control already installed install both packages
Else install package control first from here (https://packagecontrol.io/installation)
If you don’t know how to install a package follow this (https://packagecontrol.io/docs/usage)

## Information Flow

**Controller -> View -> User -> Controller**

![](https://d2mxuefqeaa7sj.cloudfront.net/s_8B654265D37658BE35153CE2BBF96ABD8F6F06BEF7B1CD7097075EE4E9C273BA_1506955682001_image.png)


**Request Body**
req.body
To access the body of a post request we need to add a package with some functionalities to Express (middlewares). To add such functionality you need to install the package in your project.

    > npm install body-parser --save
    // Body parser for forms
    var bodyParser= require('body-parser')
    // Set up middleware
    app.use(bodyParser.urlencoded({extended: true}))
    app.use(bodyParser.json())
    // Now we have access to the body through the req.body object
    app.post('/hello', function (req, res) {
    res.send('Hello ' + req.body.name + '. Your age is: '+ req.body.age)
    })

Name your inputs
The key of each property in the `req.body` will depend on the attribute of the name input. According to HTML specifications only named inputs will have their values passed when submitting a field.

    <form action="/form" method="post">
    Name: <input type="text" name="fullname"><br>
    Email: <input type="text" name="email"><br>
    <input type="submit" value="Submit">
    </form>

The `req.body` will now be

    req.body //=> {fullname: ..., email: ...}

**res.redirect()**
Redirects to the URL derived from the specified path:
**Example:**

    app.get('/',function(){
    //do something!
    res.redirect('/home')
    })

**EJS example**
app.js

    var express = require('express'),
    //requiring express
    app = express(),
    //assigning express executed as a function to the variabl app
    bodyParser = require('body-parser');
    //requiring body-parserz
    //body parser set-up (always the same)
    app.use(bodyParser.urlencoded({extended: true}))
    app.use(bodyParser.json());
    app.get('/',(req,res)=>{
    res.render('index.ejs')
    })
    //root route
    app.post('/',(req,res)=>{
    //post route
    var name = req.body.name;
    //get data from te body
    res.render('name.ejs',{name})
    //render the file name.ejs passing the variable along
    })
    app.listen(3000,()=>{
    //listeing on port 3000!
    console.log("lisening on port 3000")
    })

index.ejs

    <div>
    <form action="/" method="post">
    <!-- action determins which route will be triggered-->
    <input type="text" name="name" placeholder="name">
    <!-- assigning the name we can then get the value from req.body using body parser-->
    <input type="submit">
    </form>
    </div>

name.ejs

    <h1>Hello <% if (name) { %>
    <!--display the value of the var we passed along from our
    post route-->
    <%=name%>
    <% } %>
    from ejs</h1>

## Exercise

Use your MovieDB App, and add a UI using EJS.
You can use the original API.

