Faker.js is a JavaScript library for generating fake data. Fake data is useful when building and testing our 
application. The faker.js can generate fake data for various areas, including address, commerce, company, date, 
finance, image, random, or name.

First we need to install faker 

```
npm install faker --save
```

then we import faker in the file where we want to use it

```javascript
const faker = require('faker')
```

The const faker we'll give us access to 16 categories : 

* address
* commerce
* company
* database
* date 
* fake
* finance
* hacker
* helpers
* image
* internet
* lorem
* name 
* phone
* random
* system

which in turn give us access to several method to create fake data.

For instance , to create a user we can:

```javascript
const user = {
    first_name : faker.name.firstName(),
    last_name  : faker.name.lastName(),
    email      : faker.internet.email(),
    country    : faker.address.country(),
    address    : faker.address.streetAddress(),
    city       : faker.address.city(),
    phone      : faker.phone.phoneNumber()    
}
```

We can also create a list of users, looping as many times as the number of users 
that we want to create: 

```javascript
const users = [];

for( var i = 0; i < 50; i++ ){
    users.push(user)
}
```

And eventually insert them in the database:

```javascript
// require the users schema and faker
const Users = require('../models/users.model');
const faker = require('faker')
// create a route to create fake users
const create_users = async (req,res) => {
    try{
        const users = []
        for(var i = 0; i < 50; i ++){
            users.push({
                first_name : faker.name.firstName(),
                last_name  : faker.name.lastName(),
                email      : faker.internet.email(),
                country    : faker.address.country(),
                address    : faker.address.streetAddress(),
                city       : faker.address.city(),
                phone      : faker.phone.phoneNumber()    
        }
        const created = await User.create(users)
        res.json({ok:true,message:'Fake users successfully created'})
    }catch( error ){
        console.log(error)
        res.json({ok:false,error})
    }
}
```

See the documentation here:

https://www.npmjs.com/package/faker