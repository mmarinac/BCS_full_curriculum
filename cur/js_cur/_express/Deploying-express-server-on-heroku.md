# Deploying express app on Heroku

This option could be useful if you want to host server on heroku and client somewhere else, for example on Surge. Or you need a server for the mobile app which would be published on App Store or Google Play. 

---

<!-- <details>
    <summary>🎬 Deploying your app with Digital Ocean</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/IIqYjklZLMM?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details> -->

---

1. Install Heroku CLI: https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up 

2. In the server's root folder check that `package.json` file has `"main": "index.js"` pointing to your main server file. So if you main file is index.js then it will be `"main": "index.js"`, if your main file is called server.js it should be `"main": "server.js"`, etc.

3. Add script `"start": "node index.js"` (provided your main server file is called `index.js`) into the `scripts` section of package.json it so it will look like this:

```javascript
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index.js"
  },
```

4. Specify node engine version according to the version you have locally (you can check it form the terminal with `node -v` command). So for example in case you have version 14 add this to your `package.json`:

```javascript
  "engines": {
    "node": "14.x"
  },
```
Now your `package.json` file will look something like this:
```json
{
  "name": "multylang",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index.js"
  },
  "engines": {
    "node": "14.x"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "body-parser": "^1.19.0",
    "cors": "^2.8.5",
    "express": "^4.17.1"
  }
}
```

5. Make sure that you use port evironment variable for the port number of your server to run at:

```javascript
let port = process.env.PORT || 3030
app.listen(port, () => console.log(`I am on port ${port}`))
```


6. From the server folder run `npm i cors` and add this to your main server file:

```javascript 
let cors = require('cors')
app.use(cors())
```

7. Delete any `package-lock.json` or `yarn.lock` files you might have. 

## From the root project's folder:

> If you have not initialized your server as a git project do it now with `git init`

Run:
```
git add .
git commit -m "heroku deploy"
```

8. Create an account at heroku.com if you do not have it yet. In the terminal from the root folder of your project run `heroku login` and login in the browser to your heroku account.

9. In the terminal run `heroku create` from inside your server's root folder.

10. In the browser in the dashboard of heroku click on your newly created app and go to the "Deploy" section. 

11. Scroll down to the "Deploy using Heroku Git" section to the line similar to `heroku git:remote -a murmuring-sea-91732` there `murmuring-sea-91732` would be the name of your app. 

12. Run this line in the terminal like  
```
heroku git:remote -a murmuring-sea-91732
```

13. Run `git push heroku main` 

14. Wait for the code in the terminal to finish and you will see url with your server deployed. Go to this url and start using your server 🤘👍🚀








