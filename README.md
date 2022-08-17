# Setting up and running curriculum

Make sure you have Node.js and Git ([GitBash](https://gitforwindows.org) for Windows) installed.

The curriculum is available for you at this link: http://gk3000.gitlab.io/js_curriculum/. You can use it right from gitlab as any normal website but you need to be logged in to gitlab with an email you gave to us to have access to it. Sometimes after some idle time you will need to refresh the page if it gives 404 error for the browser to authenticate again with GitLab. 

You can also install and run it locally on your laptop with by following these steps:

In the terminal:

Navigate to the folder where you want to have your curriculum installed. Then:

## To install (just once):
1. `git clone https://gitlab.com/gk3000/js_curriculum.git`
2. `cd js_curriculum`
3. `sudo npm run setup` on Mac (you will be asked for your laptop's password) or `npm install -g docsify-cli` on Windows

## To start:
From the terminal navigate to your `js_curriculum` folder and from there run

`npm start`

Open [localhost:13666](http://localhost:13666) in your browser

## [Video tutorial](https://youtu.be/FFc-H52HtY0)