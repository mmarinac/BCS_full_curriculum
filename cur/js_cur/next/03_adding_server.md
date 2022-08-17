# Working with an Express server and MongoDB

In order to illustrate how to work with a server and a database we can build something really original ... a ToDo app!

So let's create a brand new project with create-next-app, and then let's install axios 
```
create-next-app next_todo_app
cd next_todo_app
npm install --save axios
```
Let's add now the following in /pages/index.js

```
import axios from 'axios'
import AddTodo from '../components/AddTodo';
export default class Movies extends React.Component{
    constructor(props){
        super(props)
            this.state ={
                todos:props.todos || []
            }
    }
    static getInitialProps = async () =>{
        const res = await axios.get('http://localhost:3001/todos')
        console.log(res.data)
        return  { todos:res.data } ;
    }
    getData = async (name) =>{
        const res = await axios.post('http://localhost:3001/todos/new',{name})
        this.setState({todos:res.data})
    }
    render(){
        console.log('state', this.state.todos)
    return(
        <div>
            <AddTodo getData ={this.getData}/>
            <ul>
                {this.state.todos.map((ele,i)=>{
                    debugger
                    return (
                        <li key={i}>
                            {ele.name}
                        </li>
                    )
                })}
            </ul>
        </div>
    )        
    }
}
```
Then let's create a AddTodo component in /components and paste this code:
```
export default class AddTodo extends React.Component {
    state ={
        name:''
    }
    handleChange = e => this.setState({name:e.target.value});
    handleSubmit = e => {
        e.preventDefault();
        let { name } = this.state;
        this.props.getData(name);
        this.setState({name:''})
    }
    render(){
        let { name } = this.state, 
        { handleChange, handleSubmit } = this;
        return(
            <form onSubmit ={handleSubmit}>
                <input onChange={handleChange} value={name}/>
                <button>
                    Add Todo
                </button>
            </form>
        )        
    }
};
```

Now we can create our server folder:

```
mkdir server
cd server
```
and running the following commands we will give a structure to our server :
```
touch index.js
mkdir routes
cd routes 
touch todos.js
cd ..
mkdir models
cd models
touch todos.js
```
Now let's go back to the root directory and install all the npm packages we need for the server running : 

```
npm install --save express body-parser next mongoose cors
```

Now let's add some almost standard express boiler plate code in index.js

```
const express = require('express')
const next = require('next')
const bodyParser = require('body-parser')
const PORT = process.env.PORT || 3001
const dev = process.env.NODE_DEV !== 'production' //true false
const nextApp = next({ dev })
const handle = nextApp.getRequestHandler() //part of next config
const mongoose = require('mongoose')
const cors = require('cors')

// connecting to mongo and checking if DB is running
async function connecting(){
try {
    await mongoose.connect('mongodb://127.0.0.1/my_new_todos_next_db', { useUnifiedTopology: true , useNewUrlParser: true })
    console.log('Connected to the DB')
} catch ( error ) {
    console.log('ERROR: Seems like your DB is not running, please start it up !!!');
}
}
connecting()
// end of connecting to mongo and checking if DB is running
nextApp.prepare().then(() => {
    // express code here
    const app = express()
    app.use(cors());
    app.options('*', cors());
    app.use(bodyParser.json());
    app.use(bodyParser.urlencoded({ extended: true }));
    app.use('/todos', require('./routes/todos')) 
    app.get('*', (req,res) => {
        return handle(req,res) // for all the react stuff
    })
    app.listen(PORT, err => {
        if (err) throw err;
        console.log(`ready at http://localhost:${PORT}`)
    })
})
```
The above is almost standard express code if not for the 
```
nextApp.prepare()
```
By wrapping our express server in nextApp.prepare() we tell it to use next, and that's it! all the rest is pretty standard express code, but let's see it it together anyway.

./models/todos.js

```
const mongoose = require('mongoose')
const todosSchema = new mongoose.Schema({
    name:String,
});
module.exports = mongoose.model('movies', todosSchema);
```
./routes/todos.js

```
const express = require('express')
const router = express.Router()
const Todos = require('../models/todos')

router.get('/', async (req, res) => {
    res.send(await Todos.find({}));
})
router.post('/new',async (req,res)=>{
    let { name } = req.body;
    await Todos.create({name})
    return res.send(await Todos.find({}))
})

module.exports = router
```

If you look at our toDo app at this point you can notice that we have a unique package.json for
both server and client, now replacing in the script field the 
```
"dev": "next",
```
for
```
"dev": "node server/index.js",
```
we will be able to start client and server toghether by running npm run dev.