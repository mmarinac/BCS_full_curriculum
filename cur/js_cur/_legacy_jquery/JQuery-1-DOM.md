# JQuery 1 DOM

https://www.youtube.com/watch?v=DkF5dTdNWZU&


[https://youtu.be/DkF5dTdNWZU](https://youtu.be/DkF5dTdNWZU)

----------
# Objectives
- Understand DOM Manipulation
- Using the awesome jQuery to manipulate the DOM in an easier way
- JQUERY SELECT, JQUERY MANIPULATE workflow
# The DOM

**Document Object Model**
The Document Object Model is the interface between your Javascript and HTML+CSS

It defines the logical structure of documents and the way a document is accessed and manipulated. The DOM is a representation of a web page in a browser in a tree-like manner

![](https://d2mxuefqeaa7sj.cloudfront.net/s_009A8131F3DC9846896CF2AB6507AD0E33E46F7074F8F8075698B6A7479FB4E5_1501752634615_dom.jpg)


**jQuery**

> jQuery is a fast, small (~260KB), and feature-rich JavaScript library. It makes things like HTML document traversal and manipulation, event handling, animation, and Ajax much simpler with an easy-to-use API that works across a multitude of browsers


Now let’s start with a basic example, let’s create an html file, inside of which we make a box
a div with the following style.


    <style>
        div{
          width: 200px;
          height: 200px;
          background: green;
          }
    </style>

Then we can write our very first jQuery script to select our div and to change its background color to a colour of our liking.

----------

Before we can use jQuery (or any other library) we must import into our project.
to do so go to the following link and grab the cdn.
http://code.jquery.com/

    <script
      src="http://code.jquery.com/jquery-3.2.1.js"
      integrity="sha256-DZAnKJ/6XZ9si04Hgrsxu/8s717jcIzLy3oi35EouyE="
      crossorigin="anonymous"></script>

Alternatively you can download jQuery locally and import it the same way.

----------

SELECT

| jQuery                                              | JavaScript equivalent                                                                                   |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| Find element by id:
`var el = $("#element")`        | var el = document.getElementById("element")
// or
var el = document.querySelector("#element")           |
| Find element by tag name:
`var els = $("p")`        | var els = document.getElementsByTagName("p") 
// or
var els = document.querySelectorAll("p")            |
| Find element by class name:
`var els = $(".class")` | var els = document.getElementsByClassName("class") 
// or
var els = document.querySelectorAll(".class") |



    <script>
    debugger
    //this will stop the execution so that we can see that the color was originally green.
    //the $ sign represents jquery
    $("div").css('background','red') 
    debugger
    //if you prefer you can write jQuery...
    jQuery("div").css('background','blue')
    debugger
    //
    $('div').css('border-radius','100px')
    //
    debugger
    jQuery('div').css('border','13px solid green')
    //
    $('div').css('float','right')
    </script>

Try running this code and see how the box changes every time we use the .css function

In case we want to add many styles at once the most efficient way to do so is by adding, removing or toggling a class.

    .superStyle{
            background:red;
            font-size:200px;
            color:green;
            width:300px;
    }
    $( 'li' ).addClass( 'superStyle' );
    $( 'li' ).removeClass( 'superStyle' );
    $( 'li' ).toggleClass( 'superStyle' );
    //add class hidden otherwise remove it

jQuery is not only used to change css properties, it can also be used to take data from and to write data to the DOM.


    <div>
        banana
    </div>
    
    <script>
        var textFromDIv = $('div').text().trim()
        alert(textFromDIv)
        </script>

The above script will take whatever text is inside our div, trim it from extra spaces (if any) and then alert it.
Now let’s write text to our DOM.

    $('div').text('brand new text just being inserted')

this will actually write text in the DOM replacing “banana” with the new text.

Now let’s append an html element to the DOM, like an H1


    $(`<h1>Hello</h1>`).appendTo('div')

this will result in …

# Hello

Jquery is so used especially because it makes it easy to have cool animation effects, let’s append another h1 but with some animation.


    $(`<h1>i am here too</h1>`).hide().appendTo('div').show('slow');

So far we have been targeting DOM elements directly, however this is usually not really practical because we have more than one div in our webpage, so it’s best to select only the ones we need to modify or to take data from, so let’s now target by id.
if you are familiar with css from the pre course… if you will immediately recognise that the selectors for id and classes are the same

    $('#some-id') //taget by id
    <div id="some-id"></div>
    
    $('.some-class')//target by class
    <div class="some-class"></div>

**Traversing**

> Elements in JavaScript are selected according to the HTML attributes (id, class, tagname, etc)
    $( 'li' ).closest( 'ul' ); //gets closest parent of type
    $( 'li' ).parent(); //gets first parent
    $( 'li' ).before(); //gets element before
    $( 'li' ).next(); //gets element after
    $( 'li' ).siblings(); //gets all other elements from the same parent



**Looping with jQuery through the DOM**
To loop over a collection of jQuery elements use the `.each` method. The method takes a callback with 2 arguments: the index of the element, the DOM element.

    $( "li" ).each(function( index, element ) {
    ...
    });

Example

    $.each([ 52, 97 ], function( index, value ) {
    alert( index + ": " + value );
    })
    // Output:
    0: 52 
    1: 97

It's important to put the jQuery (JS) code after the HTML code to the page so that jQuery will actualy have DOM element to manipulate after they will be loaded.


    <script src="https://code.jquery.com/jquery-3.1.0.js" ></script>
    <style type="text/css">
    .hidden { // now we can add hidden to li elements with: $( 'li' ).addClass( 'hidden' );
    display: none
    }
    .red-bg {
            background-color: red
    }
    
    .green-bg {
            background-color: red
    }
    </style>
    
    <ul>
            <li> 1 </li>
            <li> 2 </li>
            <li> 3 </li>
            <ul>
                    <li> one </li>
                    <li> two </li>
                    <li> three</li>
            </ul>
    </ul>
    .get() 
    // gets pure JS nodes
    .eq
    // gets the jQuery wrapped element

Example

    
    <script src="https://code.jquery.com/jquery-3.1.0.js" ></script>
    
    <style type="text/css">
    .hidden {
            display: none;
    }
    .red-bg {
            background-color: red
    }
    
    .green-bg {
            background-color: red
    }
    
    </style>
    
    
    
    <ul>
            <li> 1 </li>
            <li> 2 </li>
            <li> 3 </li>
            <ul>
                    <li name = "hello"> one </li>
                    <li> two </li>
                    <li> three</li>
            </ul>
    </ul>
    
    
    
    <script type="text/javascript">
            $( 'li' ).eq(2).replaceWith( '<li>I Am number 2!</li>' )
            var parent = $( 'li[name="hello"]' ).closest( 'ul' );
            parent.css({"background-color": "red"})
    
            var liMod = function( index, element ) {
                    ele = $(element)
                    ele.text()
    
                    if (ele.text() === " one "){
                            ele.after("<li>I Am after number one!</li>")
                    }
                    console.log(index, element, ele, ele.text())
            } 
    
            $( "li" ).each(liMod);
    
    </script>
    <!--
    $( 'li' ).removeClass( 'hidden' );
    //add class hidden otherwise remove it
    $( 'li' ).toggleClass( 'hidden' );
    $( 'li' ).css({ 
    'font-size': '20px', // change style
    'padding-left': '20px'
    });
    
    var listItem = $( 'li' ).first().remove();
    var replacedListItem = $( 'li' ).eq(0).replaceWith( '<li>new!</li>' )
    
    $( 'li' ).closest( 'ul' ); //get closest parent of type
    $( 'li' ).parent(); //get first parent
    
    $( 'li' ).before(); //get element before
    $( 'li' ).next(); //get element after
    $( 'li' ).siblings()
    -->


# **EXERCISES**

**EXERCISE 1**

    //exercise 1
    //create an html file with a div with a class  main then append to it an h1 
    //with the text hello.
    

**EXERCISE 2**

    Write a function called addDiv that when called adds the following element 
    
    <div>This was added with jQuery</div> 
    
    before all paragraphs (p tags) inside <div id = "exerciseTest"> of the 
    html snippet shown below:
    
    <div id = "exerciseTest">
            <p>HTML DOM Tutorial</p>
            <b>adding DOM elements</b>
            <button id="button1">Click to see the effect</button>
            <p>I am the last paragraph, don't forget me!</p> 
    </div>
    
    The object here is similar to an Array of DOM Elements.

**EXERCISE 3**
Write a function called `findLi` to find all `<li>` elements that don't have the attribute `name` with value 'color' and add `<span> with no color </span>`after the element
Snippet

    <div id = "exerciseTest">
            <ul>
                    <li name="color" value="Red">Sun</li>
                    <span>Sea</span>
                    <li value="Cold Fusion">Sand</li>
                    <li name="accept" value="Evil Plans">Hill</li>
                    <span> Dale</span>
            </ul>
            <button id="button1">Click to see the effect</button>
    </div>

**EXERCISE 4**
Define a function `FindRed` that finds all inputs with a value of "Red" and change the text of the next sibling to `the value is red!`
snippet

    <div>
            <div>
                    <label>
                            <input type="radio" name="color" value="Red">
                            <span>value?</span>
                            <div></div>
                    </label>
            </div>
            <div>
                    <label>
                            <input type="radio" name="color" value="Green">
                            <span>value?</span>
                            <div></div>
                    </label>
            </div>
            <div>
                    <label>
                            <div type="radio" name="color" value="Red">
                                    <span>value?</span>
                                    <div></div>
                            </label>
                    </div>
                    <button id="button1">Click to see the effect</button>
            </div>

**EXERCISE 5**
Write a function called `findbyAttr` to find all the `div` elements with an attribute `name` that ends with 'tutorial' and set the background color to yellow.
Snippet

    <body id="exerciseTest">
            <div id="tutorial-php">
                    <p>PHP</p>
            </div>
            <div id="JAVAtutorial">
                    <p>Java</p>
            </div>
            <div id="python-tutorial">
                    <p>Python</p>
            </div>
            <button id="button1">Click to see the effect</button>
    </body>

**EXERCISE 6**
Write a function called `findDirect` that finds all labels that are direct descendants of a `form` and mark them with a dotted red border: `1px dotted red`.
Snippet

    <div id ="exerciseTest">
            <form>
                    <label for="name">Child of form:</label>
                    <input name="name" id="name">
                    <fieldset>
                            <label for="newsletter">Grandchild of form, child of fieldset:</label>
                            <input name="newsletter" id="newsletter">
                    </fieldset>
            </form>
            Sibling to form: <input name="none">
    </div>


