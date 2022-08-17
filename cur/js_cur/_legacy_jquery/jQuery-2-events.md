# jQuery 2 events

https://www.youtube.com/watch?v=N_mggUtbm5k&&index=14&list=PLryb4nu66MZcb_LqLyWo-KuVEltlOZ7nc


[https://youtu.be/N_mggUtbm5k](https://youtu.be/N_mggUtbm5k)

----------

jQuery can also  be used to take data from the user like for example in a form or just a text input…

    <body>    
        <input id="data" type="text" placeholder="enter text">
        <button class="clickMe">click me!</button>
    </body>
    <script>
    $('.clickMe').on('click',function(){
        //attach an event listener to our button with the class of clickMe
        var userInput = $('#data').val()
        //take the value from the input with the id of data
        if(userInput) {
                alert(userInput)
        //if we manage to get the data from the user then we alert it
            }
        })
        </script>

Now let’s take the user input and write it to the DOM with a little greeting…

    <script>
        $('.clickMe').on('click',function(){
        var name = $('#data').val()
        if(name) {
            $(`<h1>Hello ${name}</h1>`).appendTo('.empty').hide().show('slow')
        }
        })
    </script>

In case we may want to take data from more than one input and if we also want the user to be able to submit data pressing enter we can use a form, which works almost the same way, the only thing is we need to use a built-in method to prevent the default behaviour (page refresh) to get on the way.

      <body>
       <form id='userForm'>
        <input id="username" type="text" placeholder="username">
        <input type="text" id="password" placeholder="password">
        <button class="clickMe">click me!</button>
       </form>  
    
        <div class="empty"></div>
    </body>
    
    <script>
        $('#userForm').on('submit',function(event){
            event.preventDefault()
            //this prevents the form from refreshing the page onSubmit...
            var username = $('#username').val()
            var password = $('#password').val()
            console.log("the username is ", username,' and the password is ',password)
        })
        </script>

Now let’s make it a bit more interactive by mixing up jquery with javascript…

      <body>
       <form id='userForm'>
        <input id="username" type="text" placeholder="username">
        <input type="text" id="password" placeholder="password">
        <input type="number" id="age" placeholder="enter age">
        <button class="clickMe">click me!</button>
       </form>  
    
        <div class="empty"></div>
    </body>
    
    <script>
    $('#userForm').on('submit',function(event){
            event.preventDefault()
            //this prevents the form from refreshing the page onSubmit...
            var username = $('#username').val()
            var password = $('#password').val()
            var age      = $('#age').val()
    
            if(!username || !password || !age){
                $('.empty').append(
                `<h1>Please fill up all required fields</h1>`
                )
            }else{
                if(age < 14){
                $('.empty').append(`
                <h1 style="color:red">
                      this site is reserved for people over the age of ${age}
                </h1>
                `) 
                }else{
                    $('.empty').append(`
                    <h1>Welcome to our awesome site ${username}!</h1>
                    `)
                }
            }
                
    })
        </script>

so far we have learned how to get data from the user and how to write it to the DOM using jQuery, now let’s see how we can also remove it


        $('.empty').on('click', function(e){
            $(e.target).remove() 
        })

**EXERCISE 1**
Build a simple app for BCS. It is just a form with a single input field in which the end-user can add the full name of a student as “name surname”. Once submit is pressed, the new name and surname gets added to a list that is displayed below. The list must be a table with two columns: one column for first name and one for surname.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_009A8131F3DC9846896CF2AB6507AD0E33E46F7074F8F8075698B6A7479FB4E5_1501756368442_image.png)


**EXERCISE 2**
We just realised that we don’t need to see the full surname in the table; extend the previous exercise 1 to only display the initial of the last name.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_009A8131F3DC9846896CF2AB6507AD0E33E46F7074F8F8075698B6A7479FB4E5_1501756453249_image.png)


**EXERCISE 3**
Extend the previous exercise by making sure that the first letter of the first name and surname are capitals, even if the user inputs a lowercase by mistake.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_009A8131F3DC9846896CF2AB6507AD0E33E46F7074F8F8075698B6A7479FB4E5_1501756511852_image.png)


**EXERCISE 4**
Extend the previous exercise by adding “form-checking” to your input form. If the submit button is pressed without any value, or a value of incorrect format, an alert should open with the message: Correct format is "first name + space + surname". Any name that breaks that pattern should generate an alert.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_009A8131F3DC9846896CF2AB6507AD0E33E46F7074F8F8075698B6A7479FB4E5_1501756639178_image.png)


**EXERCISE 5**
BCS is expanding, and we are adding new bootcamps. Now we have Java, Node, PHP & C++. Add an input field to your form which allows a student to specify the course they are enrolled in. A student can be entered multiple times (for different classes). Display 4 different classlists with the name of the class at the top of each list as in the example. Also, Make a button that will show a list of all the students with no duplicate names in a separate table.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_D89312A0A421541C3F2400822C71AA495BF86B945D62F8D5F314F96FEEEA350C_1501756895754_image.png)


