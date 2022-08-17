# Deploying meteor apps on DO

1. Create Node.js Droplet
2. Connect to Droplet via SSH
3. `sudo apt-get update`
4. `sudo apt-get install nginx`
5. `cd ../../var/www/html`
6. Clone repo
7. Install meteor: `curl https://install.meteor.com/ | sh`
8. Install packages: `meteor npm install`
9.  `meteor npm install --save bcrypt`
10. Update Node.js: 
    1. `curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -`
    2. `sudo apt-get install -y nodejs`
11.  `nano /etc/nginx/sites-enabled/default`
12. Add this snippet for location / {} object:

        location / {
                proxy_pass http://localhost:3000/;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade; # allow websockets
                proxy_set_header Host $http_host;
                proxy_set_header X-Forwarded-For $remote_addr; # preserve client IP

                # this setting allows the browser to cache the application in a way compatible with Meteor
                # on every applicaiton update the name of CSS and JS file is different, so they can be cache infinitely (h$
                # the root path (/) MUST NOT be cached
                if ($uri != '/') {
                    expires 30d;
                }
            }

13. `sudo systemctl start nginx`
14. `sudo apt-get install pm2`
15. Daemonize your process to keep app running after closing terminal:
    `pm2 start npm -- start`
    where second "start" is the name of starting script in your package.json