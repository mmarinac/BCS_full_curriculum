# Local storage

---

<details>
    <summary>🎬 Video: localStorage</summary><div class='video-container'>
        <iframe src="https://www.youtube.com/embed/ABh6pmZAYG0?rel=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen ></iframe></div>
</details>

---

[Sample code from the video lesson](https://gitlab.com/snippets/1972025)

---

In order to save data permanently in memory without the need of a database, we can use the in-browser memory called local storage.
Local storage has a few simple methods that we can use to read and write.

In order to add an item to the local storage we can use the setItem method:

```
localStorage.setItem('Your key goes here', 'Your value(as string)goes here');
```
Let's see an example of how we can add an array to the local storage.
Note that before putting our array in the storage we need to make it a string using the JSON.stringify method.
```
var arr = [{name1:'Mike', name2:'Antonello'}];
localStorage.setItem('array', JSON.stringify(arr));
```
Now let's see how we can get it back using the built-in method getItem.
```
localStorage.getItem('Your key goes here');
```
Note that getting our array back we need to make it an array again using the JSON.parse method.
```
JSON.parse(localStorage.getItem('array'));
```

Now let's say we want to remove this array from the storage, we can do it with the built-in method removeItem

```
localStorage.removeItem('Your key goes here');
```
Now let's remove our array.
```
localStorage.removeItem('array');
```
The last method that we need to see is used to clear the whole localstorage in one command.

```
localStorage.clear();

```