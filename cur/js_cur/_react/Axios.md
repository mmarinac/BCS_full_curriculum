# Axios is a promise-based library used to make HTTP requests to an external or local server.

---

<details>
    <summary>🎬 Video: React -- axios</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/AoEWlLJ9CrU?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

[Sample code from the video lesson](https://gitlab.com/snippets/1969444)

---

## Promises

Imagine you are at Starbucks and want a coffee, you are going at the cashier and make your order, you will get a ticket (a promise).

Then you will get out of the line and let other customers make their order.
If they manage to make your coffee they will resolve the promise and give you the coffee.

If something goes wrong (like they are out of the beans you order) they will have to reject their promise.

Axios is a promise-based library which we can use to make requests to an internal or external API, you can think of it as our Starbucks which will take an order (our request) and either approve it or reject it.

There are 2 main types of requests we can make using axios: GET and POST. We usually use GET requests to read data and POST to write it.

# GET

Let's see an example of how to get a movie object from a free movies API using a GET request with axios.
In order for this to work we need to create a brand new react project with `create-react-app` and install axios in it.


```
create-react-app axios_example
cd axios_example
npm i --save axios
code . or subl .
npm start
```

Then replace the content of App.js with the following:

<!-- tabs:start -->

#### **Class components**

```javascript
// ===== Version 1 =====
import React, { Component } from "react";
import axios from "axios";

class App extends Component {
  state = {
    title: "",
    error: ""
  };
  componentDidMount() {
    this.findMovie("The usual suspects");
  }
  findMovie = movie => {
    let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
    axios
      .get(url)
      .then(res => {
        let { Title, Year } = res.data;
        this.setState({ title: Title, year: Year });
      })
      .catch(error => {
        debugger;
        console.log(error)
        this.setState({ error:error.message });
      });
  };
  render() {
    let { title, year } = this.state;
    return (
      <div>
         <h1>Title:{title}</h1>
        <h1>Release year:{year}</h1> 
         {this.state.error && <h1>Oops, we have an error: {this.state.error}</h1>} 
      </div>
    );
  }
}

export default App
```

#### **Function components**

```javascript
// ===== Version 1 =====
import React, {useState, useEffect} from "react";
import axios from "axios";

const App =()=> {
const [title, setTitle]=useState('')
const [year, setYear]=useState('')
const [error, setError]=useState('')

const findMovie = movie => {
  let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
  axios
    .get(url)
    .then(res => {
      debugger
      let { Title, Year } = res.data;
      setTitle(Title)
      setYear(Year)
    })
    .catch(error => {
      debugger;
      console.log(error)
      setError(error.message);
    });
};

  useEffect(()=>{
    findMovie("The usual suspects")
  },[]
  )
  
    return (
      <div>
         <h1>Title:{title}</h1>
        <h1>Release year:{year}</h1> 
         {error && <h1>Oops, we have an error: {error}</h1>} 
      </div>
    );
  }

export default App
```

<!-- tabs:end -->

---

<iframe src="https://codesandbox.io/embed/1zooyj6zvl?fontsize=14&hidenavigation=1&module=%2Fsrc%2FApp.js&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="Axios snippet v1"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

In the above example we call our find movie function on `componentDidMount`, we grab the object that comes back as the response from our GET request (res) and we access the data we are looking for through the nested data object, (`res.data`) and we place it in the state so that we can see it on the screen.

To see what is going on in more details we can put a debugger inside our `.then` and `.catch` to see what happens.

So let's replace App.js again with this version which has debuggers.

<!-- tabs:start -->
#### **Class components**

```javascript
// ===== Version 1 ( with debuggers) =====
import React, { Component } from 'react';
import axios from 'axios';

class App extends Component {
  state ={
    title:'',
    year: '',
    error:'',
  }
  componentDidMount(){
      this.findMovie('The usual suspects')
  }
  findMovie = movie => {
    let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
    axios.get(url)
    .then((res)=>{
        debugger
      let { Title, Year } = res.data;
      this.setState({ title:Title, year:Year})
    })
    .catch((error)=>{
      debugger
      this.setState({error:'something went wrong'})
    })
  }
  render() {
    let { title, year } = this.state;
    return (
        <div>
            <h1>Title:{title}</h1>
            <h1>Release year:{year}</h1>           
        </div> 
    );
  }
}

export default App;
```

#### **Function components**

```javascript
// ===== Version 1 ( with debuggers) =====
import React, { useState, useEffect } from "react";
import axios from "axios";

const App = () => {
  const [state, setState] = useState({
    title: "",
    year: ""
  });
  const [errorMessage, setErrorMessage] = useState("");

  const findMovie = (movie) => {
    let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
    axios
      .get(url)
      .then((res) => {
        debugger
        let { Title, Year } = res.data;
        setState({ title: Title, year: Year });
      })
      .catch((error) => {
        debugger
        setErrorMessage(error.message);
      });
  };

  useEffect(() => {
    findMovie("The usual suspects");
  }, []);

  return (
    <div>
      <h1>Title:{state.title}</h1>
      <h1>Release year:{state.year}</h1>
      {errorMessage&&<h1>Oops, something went wrong: {errorMessage}</h1>}
    </div>
  );
};

export default App;
```
<!-- tabs:end -->

<iframe src="https://codesandbox.io/embed/5019q84rl?fontsize=14" title="Axios snippet v1 with debuggers" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

We can now stop the execution and examine in detail the response object (`res`) or the error if something went wrong.
In the above example we should get the `res` as there shouldn't be any errors. We can however get an error simply by tempering with the URL.

Let's replace the URL with this version:

```
let url = `httpz://omdbapi.com?t=${movie}&apikey=thewdb`;
```
We should now get a  

 ```Network Error```

 But what happens if we simply don't find any movie? We still get our response only this time it will contain the error message:

```
res.data.Error
"Movie not found!"
```

Now let's create a second version to replace App.js, this time we can dynamically find movies using the data coming from a user input so we can look for the movie we want.

<!-- tabs:start -->

#### **Class components**

```javascript
// ===== Version 2 =====
import React, { Component } from 'react';
import axios from 'axios';

class App extends Component {
  state ={
    title:'',
    error:'',
    movie:''
  }
  handleChange = e => this.setState({movie:e.target.value});
  handleSubmit = e => {
    e.preventDefault();
    let { movie } = this.state;
    this.findMovie(movie);
  }
  findMovie = movie => {
    let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
    axios.get(url)
    .then((res)=>{
        let { Title, Year, Error } = res.data;
        debugger
        this.setState({ 
          title:Title, 
          year:Year, 
          movie:'', 
          error:Error
        })
    })
    .catch((error)=>{
        debugger;
        console.log(error);
        this.setState({ error: error.message });
    })
  }
  render() {
    let { title, year, error } = this.state;
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          <input 
            onChange={this.handleChange}
            value={this.state.movie}
          />
          <button>Submit</button>
        </form> 
        <div>
      {
        !error ?
        <div>
        <h1>Title: {title}</h1>
        <h1>Release year: {year}</h1> 
        </div>
      : <h1>{error}</h1>
      }         
        </div>
      </div>
    );
  }
}

export default App;
```

#### **Function components**

```javascript
// ===== Version 2 =====
import React, { useState } from 'react';
import axios from 'axios';

const App = () => {
  const [error, setError] = useState('')
  const [state, setState] = useState({
    title:'',
    year:'',
    movie:''
  })

  const handleChange = (e) => setState({ ...state, movie: e.target.value });

  const handleSubmit = (e) => {
    e.preventDefault();
    findMovie(state.movie);
  }

  const findMovie = movie => {
    let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
    axios.get(url)
    .then((res)=>{
        let { Title, Year, Error } = res.data;
        debugger
        setState({ 
          title: Title, 
          year: Year, 
          movie: '', 
        })
    })
    .catch((error)=>{
      debugger
      setError(error.message);
    })
  }

  let { title, year, movie } = state;

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input 
          onChange={handleChange}
          value={movie}
        />
        <button>Submit</button>
      </form> 
      <div>
      { !error ?
        <div>
        <h1>Title: {title}</h1>
        <h1>Release year: {year}</h1> 
        </div>
        : <h1>{error}</h1>
      }         
      </div>
    </div>
  );
}

export default App;
```

<!-- tabs:end -->

<iframe src="https://codesandbox.io/embed/yv02llvxzx?fontsize=14" title="Axios snippet v2" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

In the above snippet we grab the data from the user input while he/she types using the `onChange` event, and we put it in the state once we find the data we are looking for when `onSubmit`.

This time we also check if the movie was found or not and if it wasn't we display an error message to inform the user. We do that using a simple ternary operator condition directly inside the return.

# Final example

In this last example we can extend our little programme adding a loading screen while we are trying to fetch the movie from the API to avoid having the title and year while they have no values.

<!-- tabs:start -->

#### **Class components**

```javascript
import React, { Component } from 'react';
import axios from 'axios';

class App extends Component {
  state ={
    title:'',
    movie:'',
    isReady:false,
    loading:false,
    error:''
  }
  handleChange = e => this.setState({movie:e.target.value});
  
  handleSubmit = e => {
    e.preventDefault();
    this.setState({loading:true})
    debugger
    let { movie } = this.state;
    this.findMovie(movie);
  }
  findMovie = movie => {
    let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
    axios.get(url)
    .then((res)=>{
      let { Title, Year, Error } = res.data;
      this.setState({ title:Title, year:Year, movie:'', isReady:true, error:Error})
    })
    .catch((error)=>{
      debugger
      this.setState({error:error.message})
    })
  }
  render() {
    let { title, year, isReady, loading, error } = this.state;
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          <input 
            onChange={this.handleChange}
            value={this.state.movie}
          />
          <button>Submit</button>
        </form>
{ 
  isReady?        
  !error ? <div>
        <h1>Title:{title}</h1>
        <h1>Release year:{year}</h1>           
        </div> :<h1>{error}</h1> : 
          loading ? <img src='https://www.organizedthemes.com/wp-content/plugins/remind-me/js/loading.gif'/> 
          : null
}
       
      </div>

    );
  }
}

export default App;
```

#### **Function components**

```javascript
import React, { useState } from 'react';
import axios from 'axios';

const App = () => {
  const [isReady, setIsReady] = useState(false);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState('');
  const [movie, setMovie] = useState({
    title: '',
    year: '',
    movie: ''
  });

  const handleChange = (e) => setMovie({ ...movie, movie: e.target.value });

  const handleSubmit = (e) => {
    e.preventDefault();
    setLoading(true);
    debugger;
    findMovie(movie.movie);
  };

  const findMovie = (mov) => {
    let url = `https://omdbapi.com?t=${mov}&apikey=thewdb`;
    axios
      .get(url)
      .then((res) => {
        let { Title, Year, Error } = res.data;
        setMovie({ title: Title, year: Year });
        setError(Error);
        setIsReady(true);
      })
      .catch((err) => {
        debugger;
        console.error(err);
        setError(err.message);
        setIsReady(true);
      });
  };

  // let { title, year, isReady, loading, error } = state;
  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input onChange={handleChange} value={movie.movie} />
        <button>Submit</button>
      </form>
      {isReady ? !error ? (
        <div>
          <h1>Title:{movie.title}</h1>
          <h1>Release year:{movie.year}</h1>
        </div>
      ) : (
        <h1>{error}</h1>
      ) : loading ? (
        <img src="https://www.organizedthemes.com/wp-content/plugins/remind-me/js/loading.gif" alt="loading" />
      ) : null}
    </div>
  );
};

export default App;
```
<!-- tabs:end -->

<iframe src="https://codesandbox.io/embed/qq6w7z83qw?fontsize=14" title="Axios final version" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

# Async and await

A more modern way to handle promises is by using `async` and `await`, they are similar to the standard promise syntax that we just saw, however they are a bit nicer to work with and can make our code a bit more readable.

In order to use `async` and `await` we need to make our function asynchronous, by writing the keyword ```async``` in front of it.

Then we can make our axios call, and we can tell our code to wait for the execution of the axios call by writing the keyword ```await```.

Similarly to the standard promise syntax we need to be ready for both, the success and error case, we can do that by wrapping our axios call in a ```try and catch```.

The syntax of try and catch is very similar to that of ```.then ``` and ```.catch``` where the success case happens in the `try` and the `catch` handles the error if there is one.

Let's see our previous examples with `async` and `await`, the rest will be the same.
<!-- tabs:start -->
#### **Class components**

```javascript
// ======= Version 1 ======
import React, { Component } from 'react';
import axios from 'axios';

class App extends Component {
  state ={
    Title:'',
    error:'',
  }
  componentDidMount(){
      this.findMovie('The usual suspects')
  }
  findMovie = async movie => {
    let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
    try {
      const res = await axios.get(url);
      let { Title, Year } = res.data;
      this.setState({ title:Title, year:Year})      
    } catch (error) {
      this.setState({error:error.message})      
    }
  }
  render() {
    let { title, year } = this.state;
    return (
        <div>
            <h1>Title:{title}</h1>
            <h1>Release year:{year}</h1>   
            {this.state.error && <h1>Oops, we have an error: {this.state.error}</h1>}         
        </div> 
    );
  }
}

export default App;
```

#### **Function components**

```javascript
// ======= Version 1 ======
import React, { useEffect, useState } from 'react';
import axios from 'axios';

const App = () => {
  const [movie, setMovie] = useState({
    title: "",
    year: ""
  })
  const [error, setError] = useState("")

  useEffect(() => {
    const findMovie = async movie => {
      let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
      try {
        const res = await axios.get(url);
        let { Title, Year } = res.data;
        setMovie({ title: Title, year: Year })
      } catch (error) {
        setError(error.message)
      }
    }
    findMovie('The usual suspects')
  }, [])

  return (
    <div>
      <h1>Title:{movie.title}</h1>
      <h1>Release year:{movie.year}</h1>
      {error && <h1>Oops, we have an error: {error}</h1>} 
    </div>
  );
}


export default App;
```

<!-- tabs:end -->

<iframe src="https://codesandbox.io/embed/j4ol5qoojw?fontsize=14" title="async and await v1" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

<!-- tabs:start -->
#### **Class components**

```javascript
// =======  Version 2 ========
import React, { Component } from 'react';
import axios from 'axios';

class App extends Component {
  state ={
    Title:'',
    error:'',
    movie:''
  }
  handleChange = e => this.setState({movie:e.target.value});
  handleSubmit = e => {
    e.preventDefault();
    let { movie } = this.state;
    this.findMovie(movie);
  }
  findMovie = async movie => {
    let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
    try {
      const res = await axios.get(url)
      let { Title, Year, Error } = res.data;
        debugger
        this.setState({ 
          title:Title, 
          year:Year, 
          movie:'', 
          error:Error
        })
    } catch (error) {
      this.setState({error:error.message})
    }
  }
  render() {
    let { title, year, error } = this.state;
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          <input 
            onChange={this.handleChange}
            value={this.state.movie}
          />
          <button>Submit</button>
        </form> 
        <div>
      {
        !error ?
        <div>
        <h1>Title: {title}</h1>
        <h1>Release year: {year}</h1> 
        </div>
      : <h1>{error}</h1>
      }         
        </div>
      </div>
    );
  }
}

export default App;
```

#### **Function components**
```javascript
// =======  Version 2 ========
import React, { useState } from 'react';
import axios from 'axios';

const App = () => {
  const [error, setError] = useState("")
  const [movie, setMovie] = useState({
    title: "",
    year: "",
    movie: ""
  })

  const handleChange = e => setMovie({ ...movie, movie: e.target.value })

  const handleSubmit = e => {
    e.preventDefault();
    findMovie(movie.movie);
  }

  const findMovie = async movie => {
    let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
    try {
      const res = await axios.get(url)
      let { Title, Year, Error } = res.data;
      debugger
      setError(Error)
      setMovie({
        title: Title,
        year: Year,
        movie: '',
      })
    } catch (err) {
      console.error(err)
      setError(err.message)
    }
  }

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input
          onChange={handleChange}
          value={movie.movie}
        />
        <button>Submit</button>
      </form>
      <div>
        {!error
          ? <div>
            <h1>Title: {movie.title}</h1>
            <h1>Release year: {movie.year}</h1>
          </div>
          : <h1>{error}</h1>
        }
      </div>
    </div>
  );
}


export default App;
```

<!-- tabs:end -->

<iframe src="https://codesandbox.io/embed/m4om3wj768?fontsize=14" title="async and await v2" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

<!-- tabs:start -->
#### **Class components**

```javascript
// =======  Version 3 ========
import React, { Component } from 'react';
import axios from 'axios';

class App extends Component {
  state ={
    Title:'',
    error:'',
    movie:'',
    isReady:false,
    loading:false,
  }
  handleChange = e => this.setState({movie:e.target.value});
  
  handleSubmit = e => {
    e.preventDefault();
    this.setState({loading:true})
    let { movie } = this.state;
    this.findMovie(movie);
  }
  findMovie = async movie => {
    let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
    try {    
      const res = await axios.get(url)
      let { Title, Year, Error } = res.data;
      this.setState({ title:Title, year:Year, movie:'', isReady:true, error:Error}) 
    } catch (error) {
      this.setState({error:error.message, isReady:true})
    }
  }
  render() {
    let { title, year, isReady, loading, error } = this.state;
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          <input 
            onChange={this.handleChange}
            value={this.state.movie}
          />
          <button>Submit</button>
        </form>
{ 
  isReady?        
  !error ? <div>
        <h1>Title:{title}</h1>
        <h1>Release year:{year}</h1>           
        </div> :<h1>{error}</h1> : 
          loading ? <img src='https://www.organizedthemes.com/wp-content/plugins/remind-me/js/loading.gif'/> 
          : null
}
       
      </div>

    );
  }
}

export default App;
```

#### **Function components**

```javascript
// =======  Version 3 ========
import React, { useState } from 'react';
import axios from 'axios';

const App = () => {
	const [ error, setError ] = useState('');
	const [ isReady, setIsReady ] = useState(false);
	const [ loading, setLoading ] = useState(false);
	const [ movie, setMovie ] = useState({
		title: '',
		year: '',
		movie: ''
	});

	const handleChange = (e) => setMovie({ ...movie, movie: e.target.value });

	const handleSubmit = (e) => {
		e.preventDefault();
		setLoading(true);
		findMovie(movie.movie);
	};
	const findMovie = async (movie) => {
		let url = `https://omdbapi.com?t=${movie}&apikey=thewdb`;
		try {
			const res = await axios.get(url);
			let { Title, Year, Error } = res.data;
			setMovie({ title: Title, year: Year, movie: '' });
			setIsReady(true);
			setError(Error);
		} catch (error) {
			setError(error.message);
      setIsReady(true);
		}
	};

	return (
		<div>
			<form onSubmit={handleSubmit}>
				<input onChange={handleChange} value={movie.movie} />
				<button>Submit</button>
			</form>
			{isReady ? !error ? (
				<div>
					<h1>Title:{movie.title}</h1>
					<h1>Release year:{movie.year}</h1>
				</div>
			) : (
				<h1>{error}</h1>
			) : loading ? (
				<img src="https://www.organizedthemes.com/wp-content/plugins/remind-me/js/loading.gif" alt="loading" />
			) : null}
		</div>
	);
};

export default App;
```



<!-- tabs:end -->

<iframe src="https://codesandbox.io/embed/012mj4zkol?fontsize=14" title="async and await final version" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

# Passing data via params

We can pass data to a server using `axios.get`, but in order to see if it works we need to have access to the server, so let's create a very simple one.

going to a non-project directory we can create a simple express project by running:
```
mkdir express_simple_server
npm init
touch index.js
npm i --save express body-parser cors
code .
```
The we can add the following in index.js

```javascript
const app = require('express')();
const port = process.env.port || 3001;
var cors = require('cors') // to send request from different url

app.use(cors())

app.use(function(req, res, next) {
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
    res.header("Access-Control-Allow-Methods", "GET, POST, OPTIONS");

    next();
});

app.get('/:name', (req, res) => {
    res.json(req.params)
})
app.listen(port, () => console.log(`server running on port ${port}`))
```

<iframe height="400px" width="100%" src="https://repl.it/@gk3000/axiosserver?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Now our little server is ready to receive some information and it will send it back to us as an object.
So let's create a request to our server and place it in react in App.js

<!-- tabs:start -->
#### **Class components**

```javascript
import React, { Component } from 'react';
import axios from 'axios';

class App extends Component {
    state= {
        name:''
    }
    componentDidMount(){
        let url = `https://axiosserver--gk3000.repl.co/John`;
        axios.get(url)
        .then((res)=>{
            let { name } = res.data;
            this.setState({name})
        }).catch((error)=>{
            debugger
        })
    }
  render() {
      let { name } = this.state;
    return (
      <div>
          <h1>hello {name}</h1>
      </div>
    );
  }
}

export default App;
```

#### **Function components**

```javascript
import React, { useEffect, useState } from 'react';
import axios from 'axios';

const App = () => {
	const [ name, setName ] = useState('');

	useEffect(() => {
		let url = `https://axiosserver--gk3000.repl.co/John`;
		axios
			.get(url)
			.then((res) => {
				setName(res.data.name);
			})
			.catch((error) => {
				debugger;
			});
	}, []);

	return (
		<div>
			<h1>hello {name}</h1>
		</div>
	);
};

export default App;
```

<!-- tabs:end -->

<iframe src="https://codesandbox.io/embed/18y641rpwq?fontsize=14" title="axios.get example w/ server" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

# POST 

We can send data using axios with a POST request, only this time we will do it through the body.
Let's first change express to be able to deal with the body.

```js
const app = require('express')();
const port = process.env.port || 3001;
var cors = require('cors') // to send request from different url


app.use(cors())

app.use(function(req, res, next) {
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
    res.header("Access-Control-Allow-Methods", "GET, POST, OPTIONS");

    next();
});

const bodyParser = require('body-parser')
app.use(bodyParser.urlencoded({
    extended: true
}))
app.use(bodyParser.json())

app.get('/:name', (req, res) => {
    res.status(200).send(req.params)
})
app.post('/', (req, res) => {
    res.status(200).send(req.body)
})
app.listen(port, () => console.log(`server running on port ${port}`))
```

<iframe height="400px" width="100%" src="https://repl.it/@gk3000/axiospostserver?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Then we can change slightly the request from axios to be a POST request and to send data via the body.

<!-- tabs:start -->
#### **Class components**

```javascript
import React, { Component } from 'react';
import axios from 'axios';

class App extends Component {
    state= {
        name:''
    }
    componentDidMount(){
        let url = `https://axiosserver--gk3000.repl.co`;
        axios.post(url, {name:'Micheal'})
        .then((res)=>{
            let { name } = res.data;
            this.setState({name})
        }).catch((error)=>{
            debugger
        })
    }
  render() {
      let { name } = this.state;
    return (
      <div>
          <h1>hello {name}</h1>
      </div>
    );
  }
}

export default App;
```

#### **Function components**

```javascript
import React, { useEffect, useState } from 'react';
import axios from 'axios';

const App = () => {
	const [ name, setName ] = useState('');

	useEffect(() => {
		let url = `https://axiosserver--gk3000.repl.co`;
		axios
			.post(url, { name: 'Micheal' })
			.then((res) => {
				setName(res.data.name);
			})
			.catch((err) => {
				debugger;
				console.error(err);
			});
	}, []);

	return (
		<div>
			<h1>hello {name}</h1>
		</div>
	);
};

export default App;
```
<!-- tabs:end -->

<iframe src="https://codesandbox.io/embed/1z22m71zj4?fontsize=14" title="axios.post example w/ server" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

## Using HTTP Headers in Axios

Even if is not considered wrong to send the authentication token in the body object, it is considered a better practice
to send it in the Authorizzation HTTP header.

We can set the Authorization HTTP header, in axios, with the authentication token, using the following syntax: 
```
axios.defaults.headers.common['Authorization'] = token
```
and we can retrieve it in the server from the request object:
```
const token = request.headers.authorization;
```