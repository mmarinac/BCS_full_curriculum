> 💥 For your web app project you can implement your own idea or choose one of the projects from this list. In any case it is important to talk to your mentors first to evaluate if the chosen project is the best choice for you based on the time-frame and you current progress

At [this page](https://projects.barcelonacodeschool.com/) you can check some of the projects done by our students during the bootcamp. 

---

# List of suggested projects:

# 1. eCommerce (full-stack)

[Boilerplate repo](https://gitlab.com/barcelonacodeschool/ecommerce_boilrplate)

### Core functionality
- register admin
- login admin
- logout admin
- add products 
- remove products
- update products
- show all product
- show one product
- add product to cart
- cart page
- remove product from cart
- increase product quantity in cart
- decrease product quantity in cart
- clear cart
- go to checkout page
- payment (stripe)
- send email confirmation
- update stock

### Extra functionality ideas
- create new admins (must be logged in as admin)
- register user
- login user
- logout user
- update user profile
- see orders done by userid
- sort orders by date
- send confirmation email user
- password reset
- add categories
- remove categories
- update categories
- create order
- admin dashboard
- show orders
- change order status
- group products by category
- filter products in price range
- combine filters
- sort products by price (asc/desc)
- sort products alphabetically (asc/desc)


 
# 2. Blog (full-stack)

[Boilerplate repo](https://gitlab.com/barcelonacodeschool/blog_boilerplate)

### Core functionality for the users
* register
* login 
* logout 
* create posts
* show all posts
* show single post 
* create a new comment associated with a post
* show all comments

### Extra
* blog posts categories (topics)

### Admin area    
* see all posts by user
* see all post by topic
* see all users
* remove users
* temporarily block users

### Extra functionality
For the admin:
* remove post         
* remove comments    
* update posts  
* update comments  
* show posts grouped by topic   
* sort post / comments by date (ascending/ descending)
* send confirmation email when registering 
* account must be confirmed via email before granting user access
* add pictures to user account 
* send email to the admin when a new post is created
* send email to the admin when a new comment is created
* moderate posts/ comments

For a user in the user area:
* show posts filtered by your user id
* update account details including picure
* remove post         
* remove comments    
* update posts  
* update comments 


# 3. SlideShow (client only)

* Create a reusable React component which accepts an array of images (URLs) and a time (via props).
* It will then display them in a slide show (you must create it from scratch).
* The slide show should change pictures automatically using the time props to determine the frequency and also allow the user to change them manually using the next and previous buttons.


# 4. Movie DB (client only)

* Create an input field from which the user can write a movie title.
* Send a request to the provided API including the title provided by the user.
* Display the movie information (choose the most important), at least title, release date, poster picture, director.
* Create a list of favorite movies which contains always the last 10 that were searched, you can store this list using the browser own localStorage.
* This list should be hidden by default and displayed with a click on the button/icon, once expanded it shows only the titles.
* Clicking on any of the titles should fetch the movie that the user clicked on and display it as if the user looked for it via the user input.

### API: 
`https://omdbapi.com/?t=${YOUR_MOVIE_TITLE_GOES_HERE}&apikey=thewdb`


# 5. Pizza ordering website (full-stack)

[Boilerplate repo](https://gitlab.com/barcelonacodeschool/pizza_website_boilerplate)

### Core functionality:

#### client 

* create and delete ingredients
* display list of ingredients
* be able to compose minimum 1 pizza with at least 3 ingredients
* display list of pizzas before the checkout 
* checkout

#### server 

* be able to create, delete and get ingredients from the database
* implement payment using stripe
* [www.stripe.com](https://stripe.com/en-es)
* [BCS stripe repo](https://gitlab.com/barcelonacodeschool/stripe_card_payments)
* create orders

### Extra functionality:

#### client

* save favorite pizzas for future orders
* create authentication ( login, register )
* user page 
* admin area

#### server 

* send emails using nodemailer ( after the payment, contact emails )
* [BCS nodemailer repo](https://gitlab.com/barcelonacodeschool/nodemailer_sending_emails)
* authentication server


# 6. Shopping cart (client only)

* Create a serverless eCommerce shopping cart part.
* It can be 2 pages: the products page with "Add to cart" button for each and the cart page itself.
* Each product should show a picture, a name and a price.
* The user should be able to add it to the cart.
* If the product is already there it should prompt the user with the option to add it again or to cancel.
* In the cart page the user should see the list of products that he added and their quantity, as well as the total cost of the order.
* The user should also be able to increase, decrease the quantity for each product in the cart and to remove it from it.
* Also there should be a "Checkout" button which should alert the user that the order is completed and display the total cost, then clear the cart.


# 7. Serverless auth (client only)

### REGISTER
* Create a purely client side authentication system using localStorage.
* You need to create a registration from with 3 inputs and one button.
* The inputs are:
  * email
  * password
  * confirm password
* All fields must be required.
* You must make sure that the email is indeed an email, and you can only accept emails from Gmail and Yahoo.
* The accepted values for the "Password" and "Confirm password" must be identical.
* The password must be at least of 8 characters, including one lowercase letter, one uppercase letter and one number.
* You should create your own encryption function to save the encrypted password and must be able to decrypt it later for the login.
  
### LOGIN
* The login form needs only two inputs and one button.
* One for the email and one for the password.
* You need to compare the email and password with these you have saved in the localStorage.
* Remember one of them is encrypted!!!.
* It should then show a message to the user, letting them know if the login was successful and greet the user by their email in case of success.


# 8. Zolzar game 

### Intergalactic battle

Create a game which will simulate a battle between people and aliens. 

You start with 5 different units for each army and each unit has 2 parameters:
- power, meaning how hard they can hit
- rate, meaning how fast they can hit

Define initial amount of each units, for example 1000.

There are 3 locations: Earth, Moon, Zolzar. The game starts on Earth, if people's army wins then next battle is on the Moon, if people win next battle is on Zolzar. If people loose the battle, next one is back on Moon or Earth. 

If any army looses battle on their home planet -- game over. 

For every battle each army can have 3 units with same amount of each, let's say 100. You need to decide a winner based on combined power, rate and total number of units. Same during each battle the units fight each other in the matching order, so unit #1 from people's army fights unit #1 from alien's army, etc. The winning unit is counted by combined power, rate and quantity. The unit which looses battle perishes entirely, the winning unit looses a certain amount of unit member which is calculated based on the damage the opposite unit causes. 

For every battle won the player can receive bonuses like new units and/pr upgrades. 

If one army runs out of unit members it looses the war. 

Add eCommerce component where you can 
– buy units if they perish
– unlock upgrades and bonuses

Use user accounts to keep progress and purchases. 

For a guest game all the purchases apply only for this current session. 

# 9. Cards against humanity game

Api: https://crhallberg.com/cah/
Gameplay: https://en.wikipedia.org/wiki/Cards_Against_Humanity

# 10. Custom lorem ipsum generator

Feel free to choose a theme and create either a server with API to use, preferable GET request so you can make it available for the public with browsers or full app with a front-end and UI. 

Examples: https://forcemipsum.com, https://hipsum.co 

# 11. Custom CSS library

Examples: https://nostalgic-css.github.io/NES.css/, http://brutalistframework.com/

# 12. Website scrapper and offline downloader 

# 13. (Video) chat

Option 1: Chat with users, similar to the one we have at barcelonacodeschool.com. There is an admin who can login to the website and guests, who see the chat module. Every guest can chat only with an admin, and the admin can chat to every client.

Option 2: Users chat -- after user signs up and login they can see a list of all users and they can invite them to chat, the other user can accept or decline. Users can also ‘friend’ other users. Extra feature — group chats.
