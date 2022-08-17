## One of the quickest way to deploy your static website is Surge.

### How does it work: 

Install Surge globally (you need to do it only once for the first time) from the terminal:

	npm install --global surge

Now from the root folder of your webpage which  you want to publish run `surge` to publish your website online:

	surge

It will ask you for your email, password and URL for your project (default generated URL would be suggested automatically).

After you published your project and if you did some changes which you need to push to the same domain, enter this:

	surge --domain YOUR_DOMAIN_OBTAINED_DURING_INITIAL_DEPLOYMENT.surge.sh

Alternatively you can create a `CNAME` file in the root of your project and type your domain name from surge in this file. By doing so all you need to run for any updates to push you new version online would be simply `surge`.

That's it! 

> To unpublish your project from Surge use this: `surge teardown YOUR_DOMAIN_NAME.surge.sh`

[![Brief video instructions on using Surge](http://img.youtube.com/vi/-EjdMvYPSVU/0.jpg)](http://www.youtube.com/watch?v=-EjdMvYPSVU "")

[Documentation](https://surge.sh/help/getting-started-with-surge)