# Using MongoDB Atlas

---

<details>
    <summary>🎬 Video: Express - using mongoDB Atlas</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/mS9cebvo_YY?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

MongoDB Atlas is online MongoDB service which allows you to use DB from remote location and in case of building the app locally and then deploying not to loose any data you have by that time in the DB. Otherwise you will start with an empty DB on the production server and fill it up again with data or will have to migrate you DB which is a tiresome process.

To use MongoDB Atlas in the same way as your local DB including Mongo shell you still need to install mongoDB locally.

## Using cloud database with&nbsp;[MongoDB Atlas](https://www.mongodb.com/cloud/atlas)

Go to https://www.mongodb.com/cloud/atlas, sign up, then create a new starter cluster, select region for the physical location of your db and start cluster.

Then create a DB user which would be your Express server app, go to config of your database in the Security --> Network access add 0.0.0.0/0 to allow incoming connections from any IP address.

In Connect section you will see a line of code to run in the Terminal to open a Mongo Shell for your remote DB and in "Connect your app" you wlll see a line of code to replace in your server from

```
 await mongoose.connect('mongodb://127.0.0.1/newdatabase' ...........
```

to something like that (it will be your own unique url)

```
 await mongoose.connect('mongodb+srv://YourAccountUserName:YourAccountPassword@cluster0-kcc0h.mongodb.net/blog-project?retryWrites=true&w=majority' ...........
```

And to open the Mongo shell from your local terminal to this remote DB instead of

```
mongo
```

you need to run (again you will see the specific url in your mLab dashboard):

```
mongo "mongodb+srv://todoapp.jptfn.mongodb.net/myFirstDatabase" --username YOURuserNAME

```

You will be asked for the database password you created before and after entering it you will be able to use mongo shell directly with your remote DB.
