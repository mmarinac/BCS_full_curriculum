# Working with dates and Date object 

> MDN Definition: JavaScript Date objects represent a single moment in time in a platform-independent format. Date objects contain a Number that represents milliseconds since 1 January 1970 UTC, https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date

Every time we work with dates it's much more convenient to use the Date object than try to manually parse data. As concluded in the definition of Date object it's a date represented by a number of milliseconds, so essentially we can see them as numbers in a linear progression going from smallest in the past to biggest in the future. 

And if they are seen as numbers it means we can use them to easily get the difference between dates to calculate all the possible ranges, countdowns and time difference between two dates. 

Let's take a look at some examples...

## Creating a current date object

```javascript
let today = new Date() // this will capture current date and time
console.log(today)
// Thu Feb 24 2022 12:10:12 GMT+0100 (Central European Standard Time)
```

## Creating a specific date object

Let's say we want to know how long ago Apollo 11 landed on the moon. For that we need to create a Date object but pass the data into it. There are several options for syntax:

```
new Date()
new Date(value)
new Date(dateString)
new Date(dateObject)

new Date(year, monthIndex)
new Date(year, monthIndex, day)
new Date(year, monthIndex, day, hours)
new Date(year, monthIndex, day, hours, minutes)
new Date(year, monthIndex, day, hours, minutes, seconds)
new Date(year, monthIndex, day, hours, minutes, seconds, milliseconds)
```

Let's take a look at couple of them:

### new Date(dateString)

With this syntax we need to pass a string in human-readable format for the date:

```javascript
var moonLanding = new Date("July 20, 1969")
console.log(moonLanding)
// Sun Jul 20 1969 00:00:00 GMT+0100 (Central European Summer Time)
```

### new Date(year, monthIndex, day)

With this syntax we pass 3 values. Pay attention that month indexes start with 0, so for January the index would be 0, for February 1 and so on...

```javascript
var moonLanding = new Date(1969, 6, 20)
console.log(moonLanding)
// Sun Jul 20 1969 00:00:00 GMT+0100 (Central European Summer Time)
```

Of course we can use variables for both examples:

```javascript
let year = 1969, month = 'July', day = 20, indexOfTheMonth = 6

var moonLanding = new Date(`${month} ${day}, ${year}`)
console.log(moonLanding)
// Sun Jul 20 1969 00:00:00 GMT+0100 (Central European Summer Time)

var moonLanding = new Date(year, indexOfTheMonth, day)
console.log(moonLanding)
// Sun Jul 20 1969 00:00:00 GMT+0100 (Central European Summer Time)
```

## Finding out time difference between two dates

Now with knowing how to create a date object we can easily find a difference between them. For example in our case to know how long ago was the first moon landing what we can do it:

```javascript
var today = new Date() // this will capture current date and time

var moonLanding = new Date("July 20, 1969")

var timeDifference = today - moonLanding

console.log(timeDifference)
// 1659961330189
```

The big number is the difference between these two dates in milliseconds. One second is a 1000 milliseconds. Now we can bring it to minutes, hours, days or years:

```javascript
var differenceInSeconds = timeDifference / 1000 
var differenceInMinutes = timeDifference / 1000 / 60
var differenceInHours = timeDifference / 1000 / 60 / 60
var differenceInDays = timeDifference / 1000 / 60 / 60 / 24 
var differenceInYears = timeDifference / 1000 / 60 / 60 / 24 / 365
```

## Comparing same date objects

As with usual objects in JavaScript comparing two Date object even if they have the same date will never be true:

```javascript
var moonLanding = new Date("July 20, 1969")
var sameDateMoonLanding = new Date("July 20, 1969")
moonLanding === sameDateMoonLanding
// false
```

So to achieve that we can transform them into string representation:


```javascript
moonLanding.toDateString() === sameDateMoonLanding.toDateString()
// true
```

## Getting/setting specific data from the Date object

We can extract any info from the Date object with built-in methods and there are plenty of them:

	.getDate()
	.getDay()
	.getFullYear()
	.getHours()
	.getMilliseconds()
	.getMinutes()
	.getMonth()
	.getSeconds()
	.getTime()
	.getTimezoneOffset()
	.getUTCDate()
	.getUTCDay()
	.getUTCFullYear()
	.getUTCHours()
	.getUTCMilliseconds()
	.getUTCMinutes()
	.getUTCMonth()
	.getUTCSeconds()

```js
// this will get a year from the date object
moonLanding.getFullYear()
// 1969
```

And there is a selection of setters methods to change some data in our date object as well:

	.setDate()
	.setFullYear()
	.setHours()
	.setMilliseconds()
	.setMinutes()
	.setMonth()
	.setSeconds()
	.setTime()
	.setUTCDate()
	.setUTCFullYear()
	.setUTCHours()
	.setUTCMilliseconds()
	.setUTCMinutes()
	.setUTCMonth()
	.setUTCSeconds()

```js
var moonLanding = new Date("July 20, 2069")
console.log(moonLanding)
// Sat Jul 20 2069 00:00:00 GMT+0200 (Central European Summer Time)

// ooops, wrong year, let's change it to 1969
moonLanding.setFullYear(1969)
console.log(moonLanding)
// Sun Jul 20 1969 00:00:00 GMT+0100 (Central European Summer Time)
```


