# Promises

---

<details>
    <summary>🎬 Video: promises, await/async</summary><div class='video-container'>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/z5LsaGUqKSs?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
</details>

---

Imagine you are at Starbucks and want a coffee, you are going at the cashier and make your order, you will get a ticket (a promise).

Then you will get out of the line and let other customers make their order.
If they manage to make your coffee they will resolve the promise and give you the coffee.

If something goes wrong (like they are out of the beans you order) they will have to reject their promise.

```js
const randomTimes = () => {
	return new Promise ((resolve, reject)=>{
		setTimeout(()=>{
			if(Math.random() > .5) {
				resolve(true);
			}else{
				resolve(false);
			}
		},1000)
	});
};
randomTimes().then((data)=>{
	console.log(data);
}).catch((err)=>{
	console.log(err);
});
```

<iframe src="https://codesandbox.io/embed/promises-1-8ngkk?autoresize=1&expandDevTools=1&fontsize=14" title="Promises 1" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>


## Consuming data from an API with promises

```js
const getMovie = (movie) =>  fetch(`https://omdbapi.com?t=${movie}&apikey=thewdb`);

getMovie('saw').then((movie)=> {
	return movie.json().then((mov)=> {
		console.log(mov)
    })
}).catch((err)=> {
	console.log(err);
})
// {Title: "Saw", Year: "2004", Rated: "R", Released: "29 Oct 2004", Runtime: "103 min", …}
```

<iframe src="https://codesandbox.io/embed/promises-2-1rzpd?autoresize=1&expandDevTools=1&fontsize=14" title="Promises 2" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

# Async and await

```js
const getMovieAsync = async title =>{
    let myMovie = await fetch(`https://omdbapi.com?t=${title}&apikey=thewdb`);
	let movieJSON = await myMovie.json()
    console.log(movieJSON);
}
```

<iframe src="https://codesandbox.io/embed/promises-3-vd26k?autoresize=1&expandDevTools=1&fontsize=14" title="Promises 3" allow="geolocation; microphone; camera; midi; vr; accelerometer; gyroscope; payment; ambient-light-sensor; encrypted-media" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

Promises are chainable, let's see an example of how we can use the fetch method to get multiple movies using the IMDB API, push them inside an array and when we are done we can return this array with the movies.

```js
const getMovies = (movies, titles) => {
    for (var title of titles){
        fetch(`https://omdbapi.com?t=${title}&apikey=thewdb`)
        .then((movie)=> {
            movie.json().then((mov)=> { 
                return movies.push(mov)
            })
        })
    }
	return movies;
}
const movies = getMovies([],['titanic','saw', 'american pie', 'the usual suspects']);
```

We can do this in a more elegant way using the built-in method `Promise.all`.
`Promise.all` will fail if any of the promises is rejected.

```js
// with promise.all
const getMovie = (movie) =>  fetch(`https://omdbapi.com?t=${movie}&apikey=thewdb`);

const promises = [] , moviesDB = [];

for (var ele of ['titanic','saw', 'the usual suspects']){
    promises.push(getMovie(ele));
}

const getMovies = moviesDB => {
    Promise.all(promises)
    .then( movies => {
        movies.forEach( mov => {
            mov.json().then( mov => {
                moviesDB.push(mov)
            })	
        })
    })
	return moviesDB;
}
const movies = getMovies(moviesDB)
```

## Handling possible errors in the requests

To find if there is a network error in the request itself (like wrong URL or wrong API key for instance) we can add `.catch` to our `getMovie` function.

In case the request itself was ok but the search didn't work (for example a movie not found) we need to check the response status.

```js
var getMovie = (movie) =>  fetch(`https://omdbapi.com?t=${movie}&apikey=thewdb`);
var promises = [] , moviesDB = [];
for (var ele of ['titanicaa']){
    promises.push(getMovie(ele));
}
var getMovies = moviesDB => {
    Promise.all(promises)
    .then((movies)=>{
        movies.forEach((mov)=> {
            mov.json().Title
            ? moviesDB.push(mov)  
            : Promise.reject('banana')
        })
    })
    return moviesDB;
}
var movies = getMovies(moviesDB)
```

You can try the previous 3 examples in the Chrome dev console.
