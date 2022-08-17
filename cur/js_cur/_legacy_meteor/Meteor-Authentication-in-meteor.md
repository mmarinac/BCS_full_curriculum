# Meteor: Authentication in meteor

[Videolesson](https://youtu.be/bSrK_F9UYxY)

----------

In meteor authentication is very simple as there is a fantastic package we can use that makes our life easier than in other frameworks.

let’s start by installing this package:


    meteor add accounts-password

Now the Account.createUser usually runs in the client, however if you need some security over users is wise to disable that feature and make sure that accounts can only be created, and updated from the server.
in order to disable that we just need to pass this fucntion to our server file.


    /server/main.js


    Accounts.config({
      forbidClientAccountCreation: true
    });

Now let’s create our method to add users .


    /server/methods/userMethods.js



## **REGISTER**
    import {Accounts}       from 'meteor/accounts-base'
    import { Meteor }       from 'meteor/meteor'
    
    Meteor.methods({
        createUserInServer: function (email, password) {
              Accounts.createUser({ email, password})
        }
    
    })

The above code will create an account using the provided email and password and will then encrypt the password so that should someone have access to our DB the user password won’t be compromised.

now all we need to do is to call this method from the client with :


    Meteor.call(name_of_the_method, options)


## **LOGIN**

Now we can login the user from the client side.


    Meteor.loginWithPassword( 
            {email},password,(err=>{
                  if(err){
                      //handle error
                      //try putting a debugger here to start with so that
                       //you can see what the error is.
                  }else{
              //handle success 
              //maybe displaying a success message?
                  }
            })
    )       


## **LOGOUT**

The logout part is even easier, all you need to do is to run

    Meteor.logout()

We can verify if the user is logged in or logged ou with the following function


    Meteor.userId()

if the user is logged out it will return null, else it will return the user id.

if you want you can check the all user by running the following:

    Meteor.user()

This will return the user including id, email, and other properties if you added any.

for example it may be useful when creating an account to add a profile property to it, with for instance full name, and username.


    let profile = {
    username:USERNAME_HERE,
    fullName:FULLNAME_HERE
    }
    
    Meteor.call('createUserInServer', email, password, profile)


# **EXERCISE**
    Create an App component which has:
    A NavBar component 
    in the navbar component there should be at list 2 pages, plus the auth pages (
    login, logout, register)
    the user must be able to register, login, and logout.
    then also create a private page which should only be accessible once logged in.
    You should still show the link to that page in the navbar but when the navbar is clicked you should display an error message saying to the user that he must be logged in to see it, of course the once the user is logged in that page should be available.
    Use the message components you should have created in the create reusable components lecture.


