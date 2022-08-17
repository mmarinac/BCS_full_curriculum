# Next.js

[Next.js](https://nextjs.org) is a javascript framework which simplifies the otherwise laborous process of server side rendering a SPA.
It uses react for the front-end and can be used with one of the many supported back-end frameworks.
Server side rendering greatly improves SEO of a site and is therefore important for most business websites.

To get started with next we can generate a boiler plate using create-next-app.
In order to use it we need to install it globally running the following command.
```
npm i -g create-next-app 
```
or if you get a permission related error you can run it with sudo privileges:
```
sudo npm i -g create-next-app
```

We can now create a new Next.js app by running in the terminal:

```
create-next-app bananaApp
```

And we can open our project in the code editor to see the code and run it by typing the following command:

```
npm run dev
```
If you are used to create-react-app, the generated content will look familiar, yet slightly different.

We now have 2 new folders: components and pages.

The pages folder is where you find all your top-level components, meaning the first component that is rendered when you reach a certain path/url.

Next uses a built-in routing system, unlike with React-router we don't need to manually specify which component is rendered when you reach a certain path.

Instead the naming of the files inside the pages folder determines which component is rendered.

So for example if we want to render a component for the about page, all we need to do is to create a React component called about.js inside the pages folder.

Let's say we want to add three pages to our little project, we want to have a home page, an about page and a contact page.

We would have to create the following files:

* index.js ==> will be rendered in the path /
* about.js ==> will be rendered in the path /about
* contact.js ==> will be rendered in the path /contact.

Now let's replace the content of ./pages/index.js with the following:

```
import React from 'react'
const Home = () => 
    <main className="hero">
      <h1 className="title">Welcome to Next!</h1>
    </main>

export default Home
```

Now let's create a new component in the folder components and let's call it layout.js, this will be rendered in all pages and will contain our header and footer, as well as being the place where we import our styles from.

Now let's add the following content to our components/layout.js

```
import Head from '../components/head'
import Nav from '../components/nav'
export default ({children, title}) => 
<div>
    <Head title = {title} />
    <Nav
        links = {[
            {href:'about', label:'about'},
            {href:'contact', label:'contact'}
        ]}
    />
    <div>
        {children}
    </div>
</div>
```
If you have been using React for a while, by now you should have noticed a nice plus in Next.js and that is that we don't need to explicitly import React in each and every component that we declare!

Now let's replace the code of /components/nav.js with the following so that we can navigate to our about and contact components:

```
import React from 'react'
import Link from 'next/link'

const Nav = ({links}) => {
  console.log(links)
  return(
  <nav>
    <ul>
      <li>
        <Link prefetch href="/">
          <a>Home</a>
        </Link>
      </li>
      <ul>
        {
          links.map((ele, i) => (
          <li key={i}>
            <Link href={ele.href}>
              <a>{ele.label}</a>
            </Link>
          </li>
        ))
        }
      </ul>
    </ul>

    <style jsx>{`
      :global(body) {
        margin: 0;
        font-family: -apple-system, BlinkMacSystemFont, Avenir Next, Avenir,
          Helvetica, sans-serif;
      }
      nav {
        text-align: center;
        background:black;
        padding: 10px;
      }
      ul {
        display: flex;
        justify-content: space-between;
        margin: 0;
        padding: 0;
      }
      nav > ul {
        padding: 4px 16px;
      }
      li {
        display: flex;
        padding: 6px 8px;
      }
      a {
        color: white;
        text-decoration: none;
        font-size: 13px;
      }
    `}</style>
  </nav>
)}

export default Nav

```

And we will add this layout component to our homepage (index.js):

```
import React from 'react'
import Layout from '../components/layout';

const Home = () => 
  <Layout>
    <main className="hero">
      <h1 className="title">Welcome to Next!</h1>
    </main>
    </Layout>

export default Home
```

Now in the about and contact components we can add in each an h1 so that we know we are rendering the correct component.

in /pages/about
```
export default () => 
    <h1>About</h1>
```
in pages/contact
```
export default () => 
    <h1>Contact</h1>
```
Now we should be able to navigate from our home page to either the about or the contact page, however when we do so our navbar disappears!
To overcome this problem we need to render the layout component also from about.js and contact.js.

in /pages/about
```
import Layout from '../components/layout';
export default () => 
    <Layout>
        <h1>About</h1>
    </Layout>
```
in pages/contact
```
import Layout from '../components/layout';
export default () => 
    <Layout>
        <h1>Contact</h1>
    </Layout>
```
Now we should be able to navigate between all our pages, awesome!

## Adding CSS to our project

In order to use standard CSS in our project we need 2 things: 

* To install a package
* To add some small piece of code in our next.config.js file
  
We first need to install a package running the following:

```
npm i --save @zeit/next-css
```
And then add this code in our next.config.js instead of default code there.

```
const withCSS = require('@zeit/next-css');
module.exports = withCSS();
```

After that you can create your CSS files and import them into your pages, components or layout component, such as:

```
import '../style/main.css';
```