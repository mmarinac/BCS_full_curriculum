# Deploying Node/React app on Digital Ocean

---

<details>
    <summary>🎬 Deploying your app with Digital Ocean</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/IIqYjklZLMM?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---

## Deploying your app

1. Sign up at http://try.digitalocean.com/developers to get some free promo credit. You will still need to provide a valid CC which would be charged after you will use all the free credit. But you can stop your droplet at any moment and you won’t be charged anything. 

2. Create a new project by following instructions on the screen after you will confirm your email. 

3. Create a new Node.js droplet by selecting Node.js template from the Marketplace. You can also create a Ubuntu droplet, then you will have to install Node manually. 

4. Choose 5$/MO for the size of your droplet with 1 GB / 1 CPU and 25 GB SSD disk.

5. Once droplet is created, you will choose the password to access this droplet later when connecting from the terminal via ssh. 

## Once you have your droplet prepare your app:

<!-- > Before deploying your projects we need to prepare them to work with your remote server, not with localhost. 

We can do it relatively easy with the following steps:

A. (LOCALLY) In your *client* create a config.js file with the following content where localhost:3000 is you port number of local server and instead of https://support.barcelonacodeschool.com/server put http://IP_ADDRESS_OF_YOUR_DROPLET/server:

```
const URL = window.location.hostname === `localhost`
            ? `http://localhost:3030`
            : `http://IP_ADDRESS_OF_YOUR_DROPLET`
            
export { URL }
```
B. (LOCALLY) Anywhere you need to send a request from your client to your server do this:

```
import { URL } from '../config'
```

And in requests themselfes use something like

```
await Axios.post(`${URL}/products/addone`,{product1})...
```

So that the request from your client will go to localhost if it's running locally or to your actual server if it's running remotely. -->

> Your server should be using `process.env.PORT` such as

        var PORT = process.env.PORT || 3000
        app.listen(PORT, function() {
            console.log(`Server is running on port ${PORT}!`)
        })

## Preparing your server to serve the optimized production build of your client

Now as we are entering the production mode we do not want to run our clients with development mode `npm start` on live server, instead we are going to make a production build and serve it instead with our main back-end express server. 

(LOCALLY) In your main back-end file (such as `server.js` or `index.js` whatever you named it) add these code `AFTER THE ROUTES`:

```javascript
const express = require('express');
const app = express();
const path = require('path');

app.use(express.static(__dirname));
app.use(express.static(path.join(__dirname, '../client/build')));

app.get('/*', function (req, res) {
  res.sendFile(path.join(__dirname, '../client/build', 'index.html'));
});
``` 

Please keep in mind that the path to your `build` folder should be your relative path from the main entry file of your server to the location of client. So if the structure of your project is like this:

![](../pics/full-stack-app-file-structure.png)

then the path from main server file `index.js` to the `build` folder would be `../client/build`

> Make sure to check [this instruction for setting up axios](/js_cur/_webdev/fs-techniques?id=setting-up-axios)


## Now continue with deployment:

6. Connect to your Digital Ocean droplet from the terminal with:

        ssh root@IP_ADDRESS_OF_YOUR_DROPLET

7. (On Digital Ocean server) You will need to type password you have chosen while creating the droplet, then press ENTER

8. (On Digital Ocean server) After login you will have access to the Ubuntu command line and control all the files and services running on your hosting server.

9. (On Digital Ocean server) You should already have git installed in the droplet, try with `git --version`, if not run `sudo apt-get install git`

10. (On Digital Ocean server) Check Node version with `node -v`, if it’s not matching your local Node version, run this to update to your current local version. If your local version is different replace number 16 with your version of node (you can check your version of node from the terminal with `node -v`):

```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
    source ~/.bashrc
    nvm install 16.13.1
    nvm use v16.13.1
```

10. (On Digital Ocean server) Run `apt-get update`

11. (On Digital Ocean server) Install web server Nginx by running `sudo apt-get install nginx`

12. (On Digital Ocean server) Go to `cd ../../var/www/html`

13. (On Digital Ocean server) Install npm packages for the client and server (if you need to install npm itself do so by running apt install npm).

14. (On Digital Ocean server) Clone your app to Digital Ocean. Go to the client folder and create a production build by running `npm run build`.

15. (On Digital Ocean server) Open Nginx config file by running `sudo nano /etc/nginx/sites-enabled/default`

16. (On Digital Ocean server) you can replace the content of `/etc/nginx/sites-enabled/default` to 

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    root /var/www/html;
    # Add index.php to the list if you are using PHP
    index index.html index.htm index.nginx-debian.html;
    server_name IP_ADDRESS_OF_YOUR_DROPLET;
    location / {
        proxy_http_version 1.1;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_pass http://localhost:1337;
    }
}
```

where port number 1337 in line `proxy_pass http://localhost:1337/;` would be your server port number. 

Also change `server_name IP_ADDRESS_OF_YOUR_DROPLET` to your droplet's IP address like `server_name 142.93.225.199;`. Later you can replace it by an actual domain name (you should also edit DNS records for the domain to point to the Digital Ocean name servers, such as `ns1.digitalocean.com, ns2.digitalocean.com, ns3.digitalocean.com`)

19. (On Digital Ocean server) Start Nginx by running `sudo systemctl start nginx`. You can also do `sudo systemctl restart nginx` and `sudo systemctl stop nginx` to restart and stop it.

19. (On Digital Ocean server) Now start your server first by running `node server.js` or how you start it normally locally to test it and make sure where are no errors. You should be able to see the client in a browser by going to IP address of your droplet and test your server from Postman by sending request to any back-end URL with your_IP_address/yourRoutes. 

20. (On Digital Ocean server) If everything is fine, install daemon `pm2` and start your server daemonized so it will be running in the background and you will have access to the console / be able to close it without stopping your apps. 

21. (On Digital Ocean server) First install it by running `sudo npm install -g pm2`

22. (On Digital Ocean server) Start your app daemonized, for example, `pm2 start server.js` from your server folder, you can also run npm scripts with pm2 by running `pm2 start npm -- start` where `start` is the name of your script. 

> To run a React app in development mode on Digital Ocean use `pm2 start node_modules/react-scripts/scripts/start.js --name "name_of_your_app"`

> After a while pm2 can create enormous log files taking gygabytes of disk space, you can dump them with `pm2 flush`. And check available space with `ncdu`, just `sudo apt-get install ncdu` it first.

23. Yay!


## Notes:

> (On Digital Ocean server) Useful error logs:

        sudo tail -30 /var/log/nginx/error.log

> (On Digital Ocean server) If you want to serve static HTML pages you might reassign a root folder by changing this record in the config file:

        root /var/www/html;

(On Digital Ocean server) So it could be something like:

        root /var/www/html/MY_WEBSITE_IS_HERE;

In this case put your files into the same folder on DO. 

# (On Digital Ocean server) Installing MongoDB on Digital Ocean (Ubuntu)

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4

    echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list

    sudo apt-get update

    sudo apt-get install -y mongodb-org


## (On Digital Ocean server) To start MongoDB:

    sudo systemctl start mongod

Run 

    nano /var/log/mongodb/mongod.log

And check if there are no errors and you can see the line

    [initandlisten] waiting for connections on port 27017

Now your DB is listenning on port 27017

## (On Digital Ocean server) To stop MongoDB:

    sudo service mongod stop

## (On Digital Ocean server) To restart MongoDB:

    sudo service mongod restart

## To open MongoDB shell:

    mongo


















