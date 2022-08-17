# React Suspense 

Official docs: https://reactjs.org/docs/concurrent-mode-suspense.html

React Suspense will display a loader if some component in the tree below is not ready yet to render. 

First we need to import Suspense from 'react', same way as useState or useEffect

```js
import React , { Suspense } from 'react'
```

Then we can wrap the component/s, that need some time to render, with the Suspense component

```js 
<Suspense fallback={<h1>Loading...</h1>}>
   <SomeComponent/>
</Suspense>
```

As you can see Suspense get a 'fallback' prop, it is required and will receive as a value the content of the loader that is going to be displayed until the wrapped component will be ready.

The content of the fallback could be a JSX tag (like the example above) or a component.


## EXAMPLE

<iframe src="https://codesandbox.io/embed/suspense-overview-vv70f?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="suspense-overview"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

We are going to fetch random foxes images from an external API, the component App.js is going to render the component Fox.js in which we are, actually, going to fetch the data from the API.

```
App.js
```

```js
// import Suspense from react
import React, { Suspense } from "react";
// import a loading package, we'll use it to display the loader
import { SemipolarLoading } from "react-loadingg";
// import the componnet that is going to fetch some data
import Fox from "./Fox";

const App = () => {
  return (
    <div>
      {/* instead of using an h1 as loader we are going to use a component */}
      <Suspense fallback={<SemipolarLoading size={"large"} color={"red"} />}>
        <Fox />
      </Suspense>
    </div>
  );
};

export default App;
```

```
Fox.js
```

```js
import React, { useState } from "react";
import axios from "axios";

// fetchFox is going to fetch a fox from the randomfox API
export function fetchFox() {
  let status = "pending";
  let result;
  let suspender = axios.get("https://randomfox.ca/floof/").then(
    r => {
      status = "success";
      result = r;
    },
    e => {
      status = "error";
      result = e;
    }
  );
  // console.log('status ==>',status)
  // console.log('suspender ==>',suspender)
  return {
    read() {
      if (status === "pending") {
        throw suspender;
      } else if (status === "error") {
        throw result;
      } else if (status === "success") {
        return result.data;
      }
    }
  };
}

// we store the result of fetchFox inside a constant that 
// we are going to use as initial state
const initial = fetchFox();

// Fox is the component itself
function Fox() {
  // in the state we are going to have the object returned by 
  // fetchFox 
  // {
  //   read(){
  //     return {
  //       image: 'some url',
  //       link : 'some link'
  //     }
  //   }
  // }
  const [resource, setResource] = useState(initial);
  debugger
  return (
    <div>
      <img src={resource.read().image} alt="random fox" />
      {/* onClick we are going to call fetchFox again and store the returned value in the state */}
      <button onClick={() => setResource(fetchFox())}>refetch fox</button>
    </div>
  )
}

export default Fox;
```
