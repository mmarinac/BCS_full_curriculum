# Set and Map 

There are 2 more data structures in JavaScript which a quite rarely used in the wild but are super handy in 2 particular cases.

## Set

`Set` objects are collections of values. You can iterate through the elements of a set in insertion order. A value in the `Set` may only occur once; it is unique in the `Set`'s collection. ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)). In other words `Set` is like an array with unique values.

While you almost never going to see `Set` used in real life, it is extremely handy in case you want to create an array of unique elements from any array. Consider this example:

```javascript
const numbers = [1,2,3,4,4,5,6,7,7,7]
const uniqueNumbers = [...new Set(numbers)]
// uniqueNumbers is [1,2,3,4,5,6,7]
```

## Map

The `Map` object holds key-value pairs and remembers the original insertion order of the keys. Any value (both objects and primitive values) may be used as either a key or a value ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)). In other words `Map` is an object with ordered key/value pairs, the order is maintained following the order of insertion. 

So apart from having a possibility to have our `Map` object truly ordered (unlike regular objects in JavaScript) there is one specific case to use `Map` other object -- the keys of `Map` do not  have to be strings. For example, they can be objects as well:

```javascript
// construct new Map object with name myMap
const myMap = new Map();
// declare some object
let mike = {name:'bob',age:20}
// add object mike as a key to myMap
myMap.set(mike, 'This string is a value, and the key is an object :)');
// get the value of object mike from myMap
myMap.get(mike)
'This string is a value, and the key is an object :)'
```
