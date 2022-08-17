## We can publish front-end app with Surge

> This is only working for client only, not suitable for the server.

### How does it work: 

Install Surge globally (you need to do it only once for the first time) from the terminal:

	npm install --global surge

Now from the root folder of your react app which you want to publish run `npm run build` to make a production optimized version of your app:

	npm run build

Then go to the `build` folder which would be created:

	cd build 

> If your react app is using router then before publishing from the `build` folder run `cp index.html 200.html`

From inside this `build` folder run `surge`:

	surge

It will ask you for your email and password if you are using surge for the first time and URL for your project (default generated URL would be suggested automatically).

After you published your project and if you did some changes which you need to push to the same domain, enter this:

	surge --domain YOUR_DOMAIN_OBTAINED_DURING_INITIAL_DEPLOYMENT.surge.sh

That's it! 

> To unpublish your project from Surge use this: `surge teardown YOUR_DOMAIN_NAME.surge.sh`

[![Brief video instructions on using Surge](http://img.youtube.com/vi/-EjdMvYPSVU/0.jpg)](http://www.youtube.com/watch?v=-EjdMvYPSVU "")

[Documentation](https://surge.sh/help/getting-started-with-surge)