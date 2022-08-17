# Passport js

# Passport.js

Simple, unobtrusive authentication for Node.js
Passport is authentication middleware for Node.js. Extremely flexible and modular, Passport can be unobtrusively dropped in to any Express-based web application. A comprehensive set of strategies support authentication using a username and password, Facebook, Twitter, and more.
Setup

    npm i --save passport passport-local-mongoose express-session

Passport makes authentication a breeze with a set of pre-defined functions.

- It effortlessly encrypts the user passwords,
- Allows us to check if the user is registered and if his string password matches the encrypted password we have saved in the DB.
- Gives us access to `req.user` so that we can check who’s logged in at all times!
    console.log(req.user.username)//Mr. Banana

It's really that simple!

![](https://d2mxuefqeaa7sj.cloudfront.net/s_C606A9D37330EB676F79DC0E5188EAB24174719BFFA1B8F2B19ADD93A09070F4_1506955959920_image.png)

    /app.js
    
    var express                        =   require('express'),
            app                                =   express(),
            LocalStrategy        =   require('passport-local'),
             passport                 =   require("passport"),
            User                        =   require('./models/User'),
            bodyParser                =   require('body-parser'),
            mongoose                =   require('mongoose');
            app.use(bodyParser.urlencoded({ extended: false }))
            
    mongoose.connect('mongodb://localhost/passport-js-simple-app');
    //===================
    // PASSPORT CONFIGURATION
    //======================
    app.use(require("express-session")({
        secret: "passport example super secret...",
        resave: false,
        saveUninitialized: false
    }));
    app.use(passport.initialize());
    app.use(passport.session());
    passport.use(new LocalStrategy(User.authenticate()));
    passport.serializeUser(User.serializeUser());
    passport.deserializeUser(User.deserializeUser());
    
    app.get('/',(req,res)=>{
            if(req.user){
                    res.send(req.user)
            }
    })
    //=======================================================
    //                                        REGISTER
    //=======================================================
    app.get("/register", function(req, res){
       res.render("register.ejs"); 
    });
    app.post("/register", function(req, res){
        var newUser = new User({
                    username: req.body.username
            });
        User.register(newUser, req.body.password, function(err, user){
            if(err){
                console.log("error", err.message);
                return res.redirect("/register");
            }
            passport.authenticate("local")(req, res, function(){
                            console.log("success", "you have successfully registered as  " + user.username);
               res.redirect("/"); 
            });
        });
    });
    //=======================================================
    //                                        LOGIN
    //=======================================================
    app.get('/login',(req,res)=>{
            res.render('login.ejs')
    })
    //handling login logic
    app.post("/login", passport.authenticate("local",
        {
            successRedirect: "/",
            failureRedirect: "/login",
        }), function(req, res){
    });
    //=======================================================
    //                                        LOGOUT
    //=======================================================
    app.get("/logout", (req, res)=>{
        req.logout();
            console.log("success", "You have successfully logged out ");
        res.redirect("/login");
    });
    
    //MIDDLEWARE TO PROTECT OUR ROUTES:
    var isLoggedIn = (req, res, next)=>{
        if(req.isAuthenticated()){return next()}
        res.redirect("/login");
    }
    app.listen(2500,( )=>{
            console.log("server running on port 2500")
    })


    /models/User.js
    
    var mongoose = require("mongoose");
    var passportLocalMongoose = require("passport-local-mongoose");
    
    var UserSchema = new mongoose.Schema({
        username: String,
        password: String,
            
    });
    
    UserSchema.plugin(passportLocalMongoose)
    const User = mongoose.model("User", UserSchema);
    module.exports = User
              

