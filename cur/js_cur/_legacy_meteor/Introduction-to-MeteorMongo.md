# Introduction to Meteor/Mongo
MongoDB is a document DB. it works much like a plain JS object and can contain all types of data structures within, even nested object. Mongoose is a further level of abstraction added to Mongo that allow us to control the data that will be added to our DB.
Classified as a [NoSQL](https://en.wikipedia.org/wiki/NoSQL) database program, MongoDB uses [JSON](https://en.wikipedia.org/wiki/JSON)-like documents and can work with or without [schemas](https://en.wikipedia.org/wiki/Database_schema).

Let’s start by creating the following folder in our root diretory

    /imports/api/todos.js

and inside the API folder let’s create a new mongo collection.
let’s name the file todo.js

## todo.js
****    import {Mongo} from 'meteor/mongo'
    export const Todos =  new Mongo.Collection('todos')

Now let’s import our collection to our /`server/main.js`


    import { Meteor } from 'meteor/meteor';
    import { Todos  } from '../imports/api/todo'
    
    Meteor.startup(() => {
      // code to run on server at startup
    });

now let’s duplicate our terminal tab so that we can play around a bit with the mongo shell and see how it works.
once in the duplicate tab with our mongo app running in the other tab let’s run the following command:

    meteor mongo

We should now be able to see the following (or a similar message)

    MongoDB shell version: YOUR_MONGO_VERSION


## Insert

We use the insert method to write into our collection

    db.todos.insert({todo:'learn meteor because it is awesome!'})
    //WriteResult({ "nInserted" : 1 })


## Remove

We use the insert method to remove from our collection

    db.todos.remove({})
    //WriteResult({ "nRemoved" : 1 })
## **Find**

We use the insert method to find the items in our collection

     db.todos.find({})
    //{ "_id" : ObjectId("59b80c2372c0f4dc8dda322b"), "todo" : "learn meteor because it is awesome!" }

to see all the collections we have in our app we can type:

    show collections

In our case we only get todos because that’s the only collection e have!

