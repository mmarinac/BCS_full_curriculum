# Mongo shell with Meteor
From your folder project run
`meteor mongo`

You will be taken to the shell of Mongo. 

After that:
`show dbs` will display a list of your databases, most likely you’d want to use `meteor` db

`use db` will take you to the selected database (instead of ‘db’ use the name of actual database

`show collections` will display a list of collections inside this db

And you can use all the regular Mongo methods:
`db.collection.find()` will find all documents in the specified ‘collection’
`db.collection.insertOne()` inserts a new document into the collection
`db.collection.insertMany()` inserts multiple new documents into the collection
`db.collection.updateOne()`   updates a single existing document in the collection
`db.collection.updateMany()` updates multiple existing documents in the collection
`db.collection.save()` inserts either a new document or update an existing document in the collection
`db.collection.deleteOne()`  deletes a single document from the collection
`db.collection.deleteMany()` deletes documents from the collection
`db.collection.drop()` drops or removes completely the collection
`db.collection.createIndex()` creates a new index on the collection if the index does not exist; otherwise, the operation has no effect
`db.getSiblingDB()` returns a reference to another database using this same connection without explicitly switching the current database. This allows for cross database queries

To learn more about working with Mongo shell use [this section](https://docs.mongodb.com/manual/mongo/) of the manual. To perform CRUD operations from the shell use [this](https://docs.mongodb.com/manual/crud/) reference.

