# Handling multiple pages in React

---

<details>
    <summary>🎬 Video: React -- handling multiple pages</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/OwfcVbC-r9s?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

Even though React makes single page applications, we often need to display more content than can possibly fit in one page, to do that we can use conditional rendering to selectively display only the component we want when we want.



    /App.js

<!-- tabs:start -->
#### **Class components**
```javascript
import React from 'react';
import './App.css';
import Home from './Home'
import About from './About'
import Contacts from './Contacts'
import Navbar from './Navbar'
import Footer from './Footer'

class App extends React.Component{

  state = {
    page:''
  }

  renderPages=(page)=>{
    this.setState({page}, ()=>{console.log(this.state)})
  }

  render(){
    return(
      <div className='App'>
      <Navbar selectPage={this.renderPages}/>

      {this.state.page === 'Home' ? 
      <Home /> : this.state.page === 'About' ? 
      <About /> : this.state.page === 'Contacts' ? 
      <Contacts /> : <Home />}

      <Footer />
      </div>
      )
  }
}

export default App;
```

#### **Function components**
```javascript
import React, { useState } from 'react';
import './App.css';
import Home from './Home';
import About from './About';
import Contacts from './Contacts';
import Navbar from './Navbar';
import Footer from './Footer';

const App = () => {
	const [ page, setPage ] = useState('');

	const renderPages = (page) => {
		setPage(page);
		console.log(page);
	};

	return (
		<div className="App">
			<Navbar selectPage={renderPages} />
			{page === 'Home' ? <Home /> : page === 'About' ? <About /> : page === 'Contacts' ? <Contacts /> : <Home />}
			<Footer />
		</div>
	);
};

export default App;

```
<!-- tabs:end -->

    /Navbar.js

```javascript
import React from 'react'

const Navbar = (props)=>{
    return <div className='navbar'>
        <ul onClick={ (e)=>props.selectPage(e.target.textContent) }>
            <li>Home</li>
            <li>About</li>
            <li>Contacts</li>
        </ul>
    </div>
}


export default Navbar
```

    /Contacts.js

```javascript
import React from 'react'

const Contacts = ()=>{
    return <h1>Contact us page / component</h1>
}


export default Contacts
```

    /Home.js

```javascript
import React from 'react'

const Home = ()=>{
    return <h1>Home page / component</h1>
}

export default Home
```

    /About.js

```javascript
import React from 'react'

const About = ()=>{
    return <h1>About us page / component</h1>
}

export default About
```

    /Footer.js

```javascript
import React from 'react'

const Footer = ()=>{
    return <footer>This is footer</footer>
}

export default Footer
```

<iframe
     src="https://codesandbox.io/embed/damp-sea-m5tf3?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="react_handling_multiple_pages"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>


## Code example to create a simple pseudo navigation with conditional rendering

<a href="js_cur/code_examples/lifecycle.zip" download>Click to Download</a>
