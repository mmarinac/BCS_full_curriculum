# HTML5

> HTML full reference: https://developer.mozilla.org/en-US/docs/Web/HTML/Element

HTML is not a programming language rather a markup language to layout content in a meaningful semantic matter. 

This is the logical structure of your page and a way to organize your content in a semantically meaningful way. It means that we do not use HTML elements for the sake of presentation, but only for telling browser that this is a heading, or paragraph, or list. In another words, to show browser what type of content we serve. 

Such as:

* paragraphs
* lists
* headings
* images
* forms
* sections and articles
* header, main and footer
* etc.

It is a terrible practice to use HTML elements purely for presentational purposes, such as "let's make this text h1 so it will be bigger". Please, don't do it. And in the opposite way, if you are listing several items use a list element instead of putting every list item in the paragraph and then trying to make them look like a list.

## Content first

Before you will start writing your HTML you need to understand the content. Analyze and structure it upfront. For sure you will have a title of the page, maybe several sections grouping the content logically, some lists, images, captions. 

As HTML elements could be nested inside each other try to not over complicate things, don't wrap them into each other if you don't really need it. Just start by writing the minimum required to assign this or that HTML tag to each content element of your page. THen later for the sake of applying CSS you might group them into some semantically meaningless containers and apply styles to the whole container. 

You start with a simple HTML boilerplate:


    <!DOCTYPE html>
    <html>
    <head>
    <!-- head section is for the meta information -->
    <title>Page Title</title>
    </head>
    <body>
    <!-- body is for the actual content -->
    <h1>This is a Heading</h1>
    <p>This is a paragraph.</p>
    </body>
    </html>

> [Check out this step by step guide to building a responsive single page](https://gitlab.com/barcelonacodeschool/css-grid-basics)

An HTML element usually consists of a **start** tag and **end** tag, with the content inserted in between:

    <tagname>Content goes here...</tagname>



The HTML **element** is everything from the start tag to the end tag:

    <p>My first paragraph.</p>

HTML elements can be nested (elements can contain elements).
All HTML documents consist of nested HTML elements.


# HTML Attributes
- All HTML elements can have **attributes**
- Attributes provide **additional information** about an element
- Attributes are always specified in **the start tag**
- Attributes usually come in name/value pairs like: **name="value"**

## The lang Attribute

The language of the document can be declared in the **`<html>`** tag.
The language is declared with the **lang** attribute.
Declaring a language is important for accessibility applications (screen readers) and search engines:

    <!DOCTYPE html>
    <html lang="en-US">
    <body>
    
    ...
    
    </body>
    </html>

## The title Attribute

We should remember always to add a title to every page we create. It will be displayed in the browser tab, bookmark of your page and **search results**.

Title also could be added to any HTML element. 

Here, a **title** attribute is added to the **<p>** element. The value of the title attribute will be displayed as a tooltip when you mouse over the paragraph:

    <p title="I'm a tooltip">
    This is a paragraph.
    </p>

## The href Attribute
    <a href="https://www.bcncoding.com">This is a link</a>

## The Size Atributes
    <img src="image.jpg" width="104" height="142">

## The alt Attribute
    <img src="bcs.jpg" alt="bcncoding.com" width="104" height="142">

## HTML Headings

Headings are defined with the `<h1>` to `<h6>` tags.
`<h1>` defines the most important heading. `<h6>` defines the least important heading.

    <h1>This is heading 1</h1>
    <h2>This is heading 2</h2>
    <h3>This is heading 3</h3>
    <h4>This is heading 4</h4>
    <h5>This is heading 5</h5>
    <h6>This is heading 6</h6>

## Headings Are Important

Search engines use the headings to index the structure and content of your web pages.
Users browse your pages by its headings. It is important to use headings to show the document structure.
`<h1>` headings should be used for main headings, followed by `<h2>` headings, then the less important `<h3>`, and so on.

**Note: Use HTML headings for headings only. Don't use headings to make text BIG or bold. Same is true for any other elements which change visual appearance -- HTML is for the structure, not for visuals.**


## The HTML `<head>` Element

The HTML **`<head>`** element has nothing to do with HTML headings.
The `<head>` element is a container for metadata. HTML metadata is data about the HTML document. Metadata is not displayed but is used by browsers and search engines.


The `<head>` element is placed between the `<html>` tag and the `<body>` tag:

    <!DOCTYPE html>
    <html>  
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <link rel="stylesheet" type="text/css" href="style.css">
        <!-- ↓↓↓ title, description, author name, keywords, og preview tags ↓↓↓ -->
        <title>My first website</title>
        <meta name="description" content="My first website">
        <meta name="author" content="GK">
        <meta name="keywords"
        content="developer, fullstack, javascript developer, web and mobile developer portfolio, fullstack developer">
        <link rel="shortcut icon" href="./images/favicon.png" type="image/x-icon">
        <meta property="og:title" content="GK portfolio page">
        <meta property="og:description" content="JavaScript Full-Stack Developer portfolio page with projects, contact information, experience and hourly rates">
        <meta property="og:image" content="http://gk3000-portfolio.surge.sh/images/gk3000.jpg">
        <meta property="og:url" content="http://gk3000-portfolio.surge.sh">
        <meta name="twitter:card" content="summary_large_image">
    </head>
        <body>
        .
        .
        .

## HTML Paragraphs

The HTML **`<p>`** element defines a **paragraph**:

    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>

## HTML Display

We never know how our pages are going to be displayed in a sense of large or small screens, desktops or mobile, resized windows, rescaled, etc. With HTML, you cannot change the output by adding extra spaces or extra lines in your HTML code.

The browser will remove any extra spaces and extra lines when the page is displayed:

    <p>
    This paragraph
    contains a lot of lines
    in the source code,
    but the browser 
    ignores it.
    </p>
    
    <p>
    This paragraph
    contains         a lot of spaces
    in the source         code,
    but the        browser 
    ignores it.
    </p>

## The Poem Problem

This poem will display on a single line:

    <p>
    Roses are red

    Violets are blue

    Unexpected curly brace

    On line 32
    </p>

## The HTML `<pre>` Element

The HTML `<pre>` element defines preformatted text.
The text inside a `<pre>` element is displayed in a fixed-width font (usually Courier), and it preserves both spaces and line breaks:

    <pre>
    Roses are red

    Violets are blue

    Unexpected curly brace

    On line 32
    </pre>

## HTML Styles
## The HTML Style Attribute

Setting the style of an HTML element, can be done with the **style attribute**.
The HTML style attribute has the following **syntax**:

    <tagname style="property:value;">

The ***property*** is a CSS property. The ***value*** is a CSS value.


    <body style="background-color:orange;">
    <h1 style="color:blue;">This is a heading</h1>
    <p style="color:red;">This is a paragraph.</p>
    <h1 style="font-family:verdana;">This is a heading</h1>
    <p style="font-family:courier;">This is a paragraph.</p>
    
    </body>

## HTML Formatting Elements

HTML also defines special **elements** for defining text with a special **meaning**.
HTML uses elements like `<b>` and `<i>` for formatting output, like **bold** or *italic* text.
Formatting elements were designed to display special types of text:


    - <b> - Bold text
    - <strong> - Important text
    - <i> - Italic text
    - <em> - Emphasized text
    - <mark> - Marked text
    - <small> - Small text
    - <del> - Deleted text
    - <ins> - Inserted text
    - <sub> - Subscript text
    - <sup> - Superscript text


    <b>This text is bold</b>
    <strong>This text is strong</strong>
    <i>This text is italic</i>
    <em>This text is emphasized</em>
    <h2>HTML <small>Small</small> Formatting</h2>
    <h2>HTML <mark>Marked</mark> Formatting</h2>
    <p>My favorite color is <del>blue</del> red.</p>
    <p>My favorite <ins>color</ins> is red.</p>
    <p>This is <sub>subscripted</sub> text.</p>
    <p>This is <sup>superscripted</sup> text.</p>


## HTML `<q>` for Short Quotations

The HTML **`<q>`** element defines a short quotation.
Browsers usually insert quotation marks around the `<q>` element.

    <p>They aim to: <q>Bring back all the best in human beings.</q></p>

## HTML `<blockquote>` for Quotations

The HTML **`<blockquote>`** element defines a section that is quoted from another source.
Browsers usually indent `<blockquote>` elements.

    <p>Here is a quote from BCS's website:</p>
    <blockquote cite="https://www.barcelonacodeschool.com">
    We teach JavaScript, Node, Express, React.js, React Native, MongoDB, Meteor. The curriculum is being constantly updated and improved based on latest tendencies and job market demand.
    </blockquote>

## HTML `<abbr>` for Abbreviations

The HTML **`<abbr>`** element defines an abbreviation or an acronym.
Marking abbreviations can give useful information to browsers, translation systems and search-engines.

    <p><abbr title="Barcelona Code School">BCS</abbr> was founded in 2016.</p>

## HTML `<address>` for Contact Information

The HTML **`<address>`** element defines contact information (author/owner) of a document or an article.
The `<address>` element is usually displayed in italic. Most browsers will add a line break before and after the element.

    <address>
    Barcelona Code School.<br> 
    Visit us at:<br>
    BCNcoding.com<br>
    Carrer de Muntaner, 262, 1-1,<br>08021 Barcelona, Spain
    </address>


## HTML `<cite>` for Work Title

The HTML **`<cite>`** element defines the title of a work.
Browsers usually display `<cite> `elements in italic.

    <p><cite>American Psycho</cite> by Bret Easton Ellis. Published in 1991.</p>

## HTML `<bdo>` for Bi-Directional Override

The HTML **`<bdo>`** element defines bi-directional override.
The `<bdo>` element is used to override the current text direction:

    <bdo dir="rtl">This text will be written from right to left</bdo>

## HTML Comment Tags

Single line

    <!-- This is a comment -->
    
    <p>This is a paragraph.</p>
    
    <!-- Remember to add more information here -->

Block coments

    <!-- Do not display this at the moment
    <img border="0" src="psycho.jpg" alt="American Psycho">
    -->

## Color Names

In HTML, a color can be specified by using a color name: red, orange, pink, yellow


## RGB Value

In HTML, a color can also be specified as an RGB value, using this formula: rgb(red, green, blue)
Each parameter (red, green, and blue) defines the intensity of the color between 0 and 255.
For example, rgb(255,0,0) is displayed as red, because red is set to its highest value (255) and the others are set to 0.
To display the color black, all color parameters must be set to 0, like this: rgb(0,0,0).
To display the color white, all color parameters must be set to 255, like this: rgb(255,255,255).


## HEX Value

In HTML, a color can also be specified using a hexadecimal value in the form: #RRGGBB, where RR (red), GG (green) and BB (blue) are hexadecimal values between 00 and FF (same as decimal 0-255).
For example, #FF0000 is displayed as red, because red is set to its highest value (FF) and the others are set to the lowest value (00).


## Styling HTML with CSS

**CSS** stands for **C**ascading **S**tyle **S**heets.
CSS describes **how HTML elements are to be displayed on screen, paper, or in other media**.
CSS **saves a lot of work**. It can control the layout of multiple web pages all at once.
CSS can be added to HTML elements in 3 ways:

- **Inline** - by using the style attribute in HTML elements
- **Internal** - by using a `<style>` element in the `<head>` section
- **External** - by using an external CSS file

The most common way to add CSS, is to keep the styles in separate CSS files. However, here we will use inline and internal styling, because this is easier to demonstrate, and easier for you to try it yourself.


## Inline CSS

An inline CSS is used to apply a unique style to a single HTML element.
An inline CSS uses the style attribute of an HTML element.
This example sets the text color of the `<h1>` element to orange:

    <h1 style="color:orange;">This is an Orange Heading</h1>

## Internal CSS

An internal CSS is used to define a style for a single HTML page.
An internal CSS is defined in the `<head>` section of an HTML page, within a `<style>` element:

    <!DOCTYPE html>
    <html>
    <head>
    <style>
    body {background-color: powderblue;}
    h1   {color: blue;}
    p    {color: red;}
    </style>
    </head>
    <body>
    
    <h1>This is a heading</h1>
    <p>This is a paragraph.</p>
    
    </body>
    </html>

## External CSS

An external style sheet is used to define the style for many HTML pages.
**With an external style sheet, you can change the look of an entire web site, by changing one file!**


To use an external style sheet, add a link to it in the `<head>` section of the HTML page:

    <!DOCTYPE html>
    <html>
    <head>
      <link rel="stylesheet" href="styles.css">
    </head>
    <body>
    
    <h1>This is a heading</h1>
    <p>This is a paragraph.</p>
    
    </body>
    </html>


An external style sheet can be written in any text editor. The file must not contain any HTML code, and must be saved with a .css extension.


Here is how the "styles.css" looks:

    body {
        background-color: black;
    }
    h1 {
        color: white;
    }
    p {
        color: pink;
    }

## CSS Fonts

The CSS **color** property defines the text color to be used.
The CSS **font-family** property defines the font to be used.
The CSS **font-size** property defines the text size to be used.


    <!DOCTYPE html>
    <html>
    <head>
    <style>
    h1 {
        color: blue;
        font-family: verdana;
        font-size: 300%;
    }
    p  {
        color: red;
        font-family: courier;
        font-size: 160%;
    }
    </style>
    </head>
    <body>
    
    <h1>This is a heading</h1>
    <p>This is a paragraph.</p>
    
    </body>
    </html>

## HTML Links - Hyperlinks

HTML links are hyperlinks.
You can click on a link and jump to another document.
When you move the mouse over a link, the mouse arrow will turn into a little hand.
**Note:** A link does not have to be text. It can be an image or any other HTML element.


## HTML Links - Syntax

In HTML, links are defined with the `<a>` tag:

    <a href="url">link text</a>
    <a href="https://www.barcelonacodeschool.com/">Barcelona Code School</a>

## Local Links

The example above used an absolute URL (A full web address). 
A local link (link to the same web site) is specified with a relative URL (without http://www....).


    <a href="banana.html">Banana page</a>

## HTML Link Colors

By default, a link will appear like this (in all browsers):

- An unvisited link is underlined and blue
- A visited link is underlined and purple
- An active link is underlined and red


You can change the default colors, by using styles:

    <style>
    a:link {
        color: white; 
        background-color: transparent; 
        text-decoration: none;
    }
    
    a:visited {
        color: orange;
        background-color: transparent;
        text-decoration: none;
    }
    
    a:hover {
        color: pink;
        background-color: transparent;
        text-decoration: underline;
    }
    
    a:active {
        color: black;
        background-color: transparent;
        text-decoration: underline;
    }
    </style>

## HTML Links - The target Attribute

The **target** attribute specifies where to open the linked document.
The target attribute can have one of the following values:

    - _blank - Opens the linked document in a new window or tab
    - _self - Opens the linked document in the same window/tab as it was clicked (this is default)
    - _parent - Opens the linked document in the parent frame
    - _top - Opens the linked document in the full body of the window
    - framename - Opens the linked document in a named frame

This example will open the linked document in a new browser window/tab:

    <a href="http://www.bcncoding.com/" target="_blank">Visit us!</a>

## HTML Links - Image as Link

It is common to use images as links:

    <a href="banana.html">
      <img src="slightly_smiling_face.gif" alt="Smiling face" style="width:42px;height:42px;border:0;">
    </a>

## HTML Images Syntax

In HTML, images are defined with the **`<img>`** tag.
The `<img>` tag is empty, it contains attributes only, and does not have a closing tag.
The `src` attribute specifies the URL (web address) of the image:

    <img src="url" alt="some_text" style="width:width;height:height;">

## The alt Attribute

The alt attribute provides an alternate text for an image, if the user for some reason cannot view it (because of slow connection, an error in the `src` attribute, or if the user uses a screen reader).
If a browser cannot find an image, it will display the value of the alt attribute:

    <img src="slightly_smiling_face.gif" alt="Image of a smiling face" style="width:600px;height:600px;">

## Image Size - Width and Height

You can use the **style** attribute to specify the width and height of an image.
The values are specified in pixels (use px after the value):

    <img src="psycho.gif" alt="American Psycho" style="width:600px;height:600px;">

Alternatively, you can use the **width** and **height** attributes. Here, the values are specified in pixels by default:

    <img src="psycho.gif" alt="American Psycho" width="600" height="600">

## Width and Height, or Style?

Both the width, height, and style attributes are valid in HTML5.
However, using the style attribute prevents internal or external styles sheets from changing the original size of images.


## Images in Another Folder

If not specified, the browser expects to find the image in the same folder as the web page.
However, it is common to store images in a sub-folder. You must then include the folder name in the src attribute:

    <img src="/images/psycho.gif" alt="American Psycho" style="width:600px;height:600px;">

Images could be located on another server as well. In this case just specify the path to it inside the `src` attribute.


## Defining an HTML Table

An HTML table is defined with the **`<table>`** tag.
Each table row is defined with the **`<tr>`** tag. A table header is defined with the **`<th>`** tag. By default, table headings are bold and centered. A table data/cell is defined with the **`<td>`** tag.



    <table style="width:100%">
      <tr>
        <th>Firstname</th>
        <th>Lastname</th> 
        <th>Age</th>
      </tr>
      <tr>
        <td>Jill</td>
        <td>Smith</td> 
        <td>50</td>
      </tr>
      <tr>
        <td>Eve</td>
        <td>Jackson</td> 
        <td>94</td>
      </tr>
    </table>


## HTML Table - Adding a Border

If you do not specify a border for the table, it will be displayed without borders.
A border is set using the CSS **border** property:

    table, th, td {
        border: 1px solid black;
    }

## HTML Table - Collapsed Borders

If you want the borders to collapse into one border, add the CSS **border-collapse** property:

    table, th, td {
        border: 1px solid black;
        border-collapse: collapse;
    }

## HTML Table - Adding Cell Padding

Cell padding specifies the space between the cell content and its borders.
If you do not specify a padding, the table cells will be displayed without padding.
To set the padding, use the CSS **padding** property:

    th, td {
        padding: 15px;
    }

## Unordered HTML List

An unordered list starts with the **`<ul>`** tag. Each list item starts with the **`<li>`** tag.
The list items will be marked with bullets (small black circles) by default:

    <ul>
      <li>Coffee</li>
      <li>Tea</li>
      <li>Milk</li>
    </ul>

## Unordered HTML List - Choose List Item Marker

The CSS **list-style-type** property is used to define the style of the list item marker:

    | Value  | Description                                     |
    | ------ | ----------------------------------------------- |
    | disc   | Sets the list item marker to a bullet (default) |
    | circle | Sets the list item marker to a circle           |
    | square | Sets the list item marker to a square           |
    | none   | The list items will not be marked               |

----------
## Ordered HTML List

An ordered list starts with the **`<ol>`** tag. Each list item starts with the **`<li>`** tag.
The list items will be marked with numbers by default:

    <ol>
      <li>Coffee</li>
      <li>Tea</li>
      <li>Milk</li>
    </ol>


## Ordered HTML List - The Type Attribute

The **type** attribute of the `<ol>` tag, defines the type of the list item marker:

    | Type     | Description                                                  |
    | -------- | ------------------------------------------------------------ |
    | type="1" | The list items will be numbered with numbers (default)       |
    | type="A" | The list items will be numbered with uppercase letters       |
    | type="a" | The list items will be numbered with lowercase letters       |
    | type="I" | The list items will be numbered with uppercase roman numbers |
    | type="i" | The list items will be numbered with lowercase roman numbers |


## HTML Description Lists

HTML also supports description lists.
A description list is a list of terms, with a description of each term.
The **`<dl>`** tag defines the description list, the **`<dt>`** tag defines the term (name), and the **`<dd>`** tag describes each term: 

    <dl>
      <dt>Coffee</dt>
      <dd>- black hot drink</dd>
      <dt>Milk</dt>
      <dd>- white cold drink</dd>
    </dl>

## Nested HTML Lists

List can be nested (lists inside lists):

    <ul>
      <li>Coffee</li>
      <li>Tea
        <ul>
          <li>Black tea</li>
          <li>Green tea</li>
        </ul>
      </li>
      <li>Milk</li>
    </ul>

## Horizontal Lists

HTML lists can be styled in many different ways with CSS.
One popular way is to style a list horizontally, to create a menu:

    <!DOCTYPE html>
    <html>
    <head>
    <style>
    ul {
        list-style-type: none;
        margin: 0;
        padding: 0;
        overflow: hidden;
        background-color: #333333;
    }
    
    li {
        float: left;
    }
    
    li a {
        display: block;
        color: white;
        text-align: center;
        padding: 16px;
        text-decoration: none;
    }
    
    li a:hover {
        background-color: #111111;
    }
    </style>
    </head>
    <body>
    
    <ul>
      <li><a href="#home">Home</a></li>
      <li><a href="#news">News</a></li>
      <li><a href="#contact">Contact</a></li>
      <li><a href="#about">About</a></li>
    </ul>
    
    </body>
    </html>

# HTML Block and Inline Elements
## Block-level Elements

A block-level element always starts on a new line and takes up the full width available (stretches out to the left and right as far as it can).
The `<div>` element is a block-level element.

Examples of block-level elements:

    - <div>
    - <h1> - <h6>
    - <p>
    - <form>


## Inline Elements

An inline element does not start on a new line and only takes up as much width as necessary.
This is an inline `<span>` element inside a paragraph.
Examples of inline elements:

    - <span>
    - <a>
    - <img>


## The `<div>` Element

The `<div>` element is often used as a container for other HTML elements.
The `<div>` element has no required attributes, but both **style** and **class** are common.
When used together with CSS, the `<div>` element can be used to style blocks of content:

    <div style="background-color:black;color:white;padding:20px;">
      <h2>London</h2>
      <p>London is the capital city of England. It is the most populous city in the United Kingdom, with a metropolitan area of over 13 million inhabitants.</p>
    </div>

# HTML The class Attribute
## Using The class Attribute

The HTML class attribute makes it possible to define equal styles for elements with the same class name.


Here we have three `<div>` elements that point to the same class name:

    <!DOCTYPE html>
    <html>
    <head>
    <style>
    div.cities {
        background-color: black;
        color: white;
        margin: 20px 0 20px 0;
        padding: 20px;
    } 
    </style>
    </head>
    <body>
    
    <div class="cities">
    <h2>London</h2>
    <p>London is the capital of England. It is the most populous city in the United Kingdom, with a metropolitan area of over 13 million inhabitants.</p>
    </div>
    
    <div class="cities">
    <h2>Paris</h2>
    <p>Paris is the capital and most populous city of France.</p>
    </div>
    
    <div class="cities">
    <h2>Tokyo</h2>
    <p>Tokyo is the capital of Japan, the center of the Greater Tokyo Area,
    and the most populous metropolitan area in the world.</p>
    </div>
    
    </body>
    </html>

## Using The class Attribute on Inline Elements

The HTML class attribute can also be used for inline elements:

    <!DOCTYPE html>
    <html>
    <head>
    <style>
    span.note {
        font-size: 120%;
        color: red;
    }
    </style>
    </head>
    <body>
    
    <h1>My <span class="note">Important</span> Heading</h1>
    <p>This is some <span class="note">important</span> text.</p>
    
    </body>
    </html>

# HTML Iframes

An iframe is used to display a web page within a web page or embed some content from another source

## Iframe Syntax

An HTML iframe is defined with the **`<iframe>`** tag:

    <iframe src="URL"></iframe>

The **src** attribute specifies the URL (web address) of the inline frame page.

# HTML JavaScript

JavaScript makes HTML pages more dynamic and interactive.

    <!DOCTYPE html>
    <html>
    <body>
    
    <h1>My First JavaScript</h1>
    
    <button type="button"
    onclick="document.getElementById('demo').innerHTML = Date()">
    Click me to display Date and Time.</button>
    
    <p id="demo"></p>
    
    </body>
    </html> 

## The HTML `<script>` Tag

The **`<script>`** tag is used to define a client-side script (JavaScript).
The `<script>` element either contains scripting statements, or it points to an external script file through the **src**attribute.
Common uses for JavaScript are image manipulation, form validation, and dynamic changes of content.
To select an HTML element, JavaScript very often use the `document.getElementById(id)` method.
This JavaScript example writes "Hello JavaScript!" into an HTML element with id="demo":

    <script>
    document.getElementById("demo").innerHTML = "Hello JavaScript!";
    </script>

## The HTML `<noscript>` Tag

The **`<noscript>`** tag is used to provide an alternate content for users that have disabled scripts in their browser or have a browser that doesn't support client-side scripts:

    <script>
    document.getElementById("demo").innerHTML = "Hello JavaScript!";
    </script>
    
    <noscript>Sorry, your browser does not support JavaScript!</noscript>

# HTML File Paths

    | Path                            | Description                                                                        |
    | ------------------------------- | ---------------------------------------------------------------------------------- |
    | <img src="picture.jpg">         | picture.jpg is located in the same folder as the current page                      |
    | <img src="images/picture.jpg">  | picture.jpg is located in the images folder located in the current folder          |
    | <img src="/images/picture.jpg"> | picture.jpg is located in the images folder located at the root of the current web |
    | <img src="../picture.jpg">      | picture.jpg is located in the folder one level up from the current folder          |


----------
## HTML File Paths

A file path describes the location of a file in a web site's folder structure.
File paths are used when linking to external files like:

- Web pages
- Images
- Style sheets
- JavaScripts

## Absolute File Paths

An absolute file path is the full URL to an internet file:

    <img src="https://www.bcncoding.com/images/picture.jpg" alt="JavaScript">

## Relative File Paths

A relative file path points to a file relative to the current page.
In this example the file path points to a file in the images folder located at the root of the current web:

    <img src="/images/picture.jpg" alt="JavaScript">

In this example the file path points to a file in the images folder located in the current folder:

    <img src="images/picture.jpg" alt="JavaScript">

In this example the file path points to a file in the images folder located in the folder one level above the current folder:

    <img src="../images/picture.jpg" alt="JavaScript">

## Best Practice

It is a best practice to use relative file paths (if possible).
When using relative file paths, your web pages will not be bound to your current base URL. All links will work on your own computer (localhost) as well as on your current public domain and your future public domains. 


# HTML Head
## The HTML <head> Element

The **`<head>`** element is a container for metadata (data about data) and is placed between the `<html>` tag and the `<body>` tag.
HTML metadata is data about the HTML document. Metadata is not displayed.
Metadata typically define the document title, character set, styles, links, scripts, and other meta information.
The following tags describe metadata: `<title>`, `<style>`, `<meta>`, `<link>`, `<script>`, and `<base>`.


## The HTML <title> Element

The **`<title>`** element defines the title of the document, and is required in all HTML/XHTML documents.
The `<title>` element:

- defines a title in the browser tab
- provides a title for the page when it is added to favorites
- displays a title for the page in search engine results


A simple HTML document:

    <!DOCTYPE html>
    <html>
    
    <head>
      <title>Page Title</title>
    </head>
    
    <body>
    The content of the document......
    </body>
    
    </html>



## The HTML `<style>` Element

The **`<style>`** element is used to define style information for a single HTML page:

    <style>
      body {background-color: powderblue;}
      h1 {color: red;}
      p {color: blue;}
    </style>

## The HTML `<link>` Element

The **`<link>`** element is used to link to external style sheets:

    <link rel="stylesheet" href="mystyle.css">

## The HTML `<meta>` Element

The **`<meta>`** element is used to specify which character set is used, page description, keywords, author, and other metadata.
Metadata is used by browsers (how to display content), by search engines (keywords), and other web services.
Define the character set used:

    <meta charset="UTF-8">

Define a description of your web page:

    <meta name="description" content="JavaScript Full-Stack Bootcamp">

Define keywords for search engines:

    <meta name="keywords" content="JavaScript, React, Node, Express">

Define the author of a page:

    <meta name="author" content="Barcelona Code School">

Refresh document every 30 seconds:

    <meta http-equiv="refresh" content="30">

Example of `<meta>` tags:

    <meta charset="UTF-8">
    <meta name="description" content="JavaScript Full-Stack Bootcamp">
    <meta name="keywords" content="JavaScript, React, Node, Express">
    <meta name="author" content="Barcelona Code School">

## Setting The Viewport

HTML5 introduced a method to let web designers take control over the viewport, through the `<meta>` tag.
The viewport is the user's visible area of a web page. It varies with the device, and will be smaller on a mobile phone than on a computer screen.
You should include the following `<meta>` viewport element in all your web pages:

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

A `<meta>` viewport element gives the browser instructions on how to control the page's dimensions and scaling.
The width=device-width part sets the width of the page to follow the screen-width of the device (which will vary depending on the device).
The initial-scale=1.0 part sets the initial zoom level when the page is first loaded by the browser.

## The HTML `<script>` Element

The `<script>` element is used to define client-side JavaScripts.
This JavaScript writes "Hello JavaScript!" into an HTML element with id="demo":

    <script>
    function myFunction {
        document.getElementById("demo").innerHTML = "Hello JavaScript!";
    }
    </script>

## The HTML `<base>` Element

The `<base>` element specifies the base URL and base target for all relative URLs in a page:

**Example**

    <base href="http://bcncoding/images/" target="_blank">


    <!DOCTYPE html>
    <html>
    <head>
      <title>Page Title</title>
      <base href="https://www.bcncoding.com/images/" target="_blank">
    </head>
    <body>
    
    <img src="html5.gif">
    <p>Since we have specified a base URL, the browser will look for the image "html5.gif" at "https://www.bcncoding.com/images/html5.gif"</p>
    
    <p><a href="https://www.bcncoding.com">BCS</a></p>
    <p>The link above opens in a new window. This is because the base target is set to "_blank".</p>
    
    </body>
    </html>
    
    

## Omitting `<html>`, `<head>` and `<body>`?

According to the HTML5 standard; the `<html>`, the `<body>`, and the `<head>` tag can be omitted.
The following code will validate as HTML5:


    <!DOCTYPE html>
    <title>Page Title</title>
    
    <h1>This is a heading</h1>
    <p>This is a paragraph.</p>

# HTML Layouts
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    div.container {
        width: 100%;
        border: 1px solid gray;
    }
    
    header, footer {
        padding: 1em;
        color: white;
        background-color: black;
        clear: left;
        text-align: center;
    }
    
    nav {
        float: left;
        max-width: 160px;
        margin: 0;
        padding: 1em;
    }
    
    nav ul {
        list-style-type: none;
        padding: 0;
    }
       
    nav ul a {
        text-decoration: none;
    }
    
    article {
        margin-left: 170px;
        border-left: 1px solid gray;
        padding: 1em;
        overflow: hidden;
    }
    </style>
    </head>
    <body>
    
    <div class="container">
    
    <header>
       <h1>City Gallery</h1>
    </header>
      
    <nav>
      <ul>
        <li><a href="#">London</a></li>
        <li><a href="#">Paris</a></li>
        <li><a href="#">Tokyo</a></li>
      </ul>
    </nav>
    
    <article>
      <h1>London</h1>
      <p>London is the capital city of England. It is the most populous city in the  United Kingdom, with a metropolitan area of over 13 million inhabitants.</p>
      <p>Standing on the River Thames, London has been a major settlement for two millennia, its history going back to its founding by the Romans, who named it Londinium.</p>
    </article>
    
    <footer>Copyright &copy;</footer>
    
    </div>
    
    </body>
    </html>
    
    

## HTML Layout Elements

Websites often display content in multiple columns (like a magazine or newspaper).
HTML5 offers new semantic elements that define the different parts of a web page:

    - <header> - Defines a header for a document or a section
    - <nav> - Defines a container for navigation links
    - <section> - Defines a section in a document
    - <article> - Defines an independent self-contained article
    - <aside> - Defines content aside from the content (like a sidebar)
    - <footer> - Defines a footer for a document or a section
    - <details> - Defines additional details
    - <summary>  - Defines a heading for the <details> element 


## HTML Layout Techniques

There are four different ways to create multicolumn layouts. Each way has its pros and cons:

- HTML tables
- CSS float property
- CSS framework
- CSS flexbox

## Which One to Choose?

**HTML Tables**
The <table> element was not designed to be a layout tool! The purpose of the <table> element is to display tabular data. So, do not use tables for your page layout! They will bring a mess into your code. And imagine how hard it will be to redesign your site after a couple of months.
**Tip:** Do NOT use tables for your page layout!
**CSS Frameworks**
If you want to create your layout fast, you can use a framework, like Bootstrap.
**CSS Floats**
It is common to do entire web layouts using the CSS float property. Float is easy to learn - you just need to remember how the float and clear properties work. Disadvantages: Floating elements are tied to the document flow, which may harm the flexibility. 


    <!DOCTYPE html>
    <html>
    <head>
    <style>
    div.container {
        width: 100%;
        border: 1px solid gray;
    }
    
    header, footer {
        padding: 1em;
        color: white;
        background-color: black;
        clear: left;
        text-align: center;
    }
    
    nav {
        float: left;
        max-width: 160px;
        margin: 0;
        padding: 1em;
    }
    
    nav ul {
        list-style-type: none;
        padding: 0;
    }
       
    nav ul a {
        text-decoration: none;
    }
    
    article {
        margin-left: 170px;
        border-left: 1px solid gray;
        padding: 1em;
        overflow: hidden;
    }
    </style>
    </head>
    <body>
    
    <div class="container">
    
    <header>
       <h1>City Gallery</h1>
    </header>
      
    <nav>
      <ul>
        <li><a href="#">London</a></li>
        <li><a href="#">Paris</a></li>
        <li><a href="#">Tokyo</a></li>
      </ul>
    </nav>
    
    <article>
      <h1>London</h1>
      <p>London is the capital city of England. It is the most populous city in the  United Kingdom, with a metropolitan area of over 13 million inhabitants.</p>
      <p>Standing on the River Thames, London has been a major settlement for two millennia, its history going back to its founding by the Romans, who named it Londinium.</p>
    </article>
    
    <footer>Copyright &copy; BCS</footer>
    
    </div>
    
    </body>
    </html>
    
    


**CSS Flexbox**
Flexbox is a new layout mode in CSS3.
Use of flexbox ensures that elements behave predictably when the page layout must accommodate different screen sizes and different display devices. Disadvantages: Does not work in IE10 and earlier.

    <!DOCTYPE html>
    <html>
    <head>
    <style> 
    .flex-container {
        display: -webkit-flex;
        display: flex;  
        -webkit-flex-flow: row wrap;
        flex-flow: row wrap;
        text-align: center;
    }
    
    .flex-container > * {
        padding: 15px;
        -webkit-flex: 1 100%;
        flex: 1 100%;
    }
    
    .article {
        text-align: left;
    }
    
    header {background: black;color:white;}
    footer {background: #aaa;color:white;}
    .nav {background:#eee;}
    
    .nav ul {
        list-style-type: none;
        padding: 0;
    }
    .nav ul a {
        text-decoration: none;
    }
    
    @media all and (min-width: 768px) {
        .nav {text-align:left;-webkit-flex: 1 auto;flex:1 auto;-webkit-order:1;order:1;}
        .article {-webkit-flex:5 0px;flex:5 0px;-webkit-order:2;order:2;}
        footer {-webkit-order:3;order:3;}
    }
    </style>
    </head>
    <body>
    
    <div class="flex-container">
    <header>
      <h1>City Gallery</h1>
    </header>
    
    <nav class="nav">
    <ul>
      <li><a href="#">London</a></li>
      <li><a href="#">Paris</a></li>
      <li><a href="#">Tokyo</a></li>
    </ul>
    </nav>
    
    <article class="article">
      <h1>London</h1>
      <p>London is the capital city of England. It is the most populous city in the United Kingdom,
      with a metropolitan area of over 13 million inhabitants.</p>
      <p>Standing on the River Thames, London has been a major settlement for two millennia,
      its history going back to its founding by the Romans, who named it Londinium.</p>
      <p><strong>Resize this page to see that what happens!</strong></p>
    </article>
    
    <footer>Copyright &copy; BCS</footer>
    </div>
    
    </body>
    </html>
    
    
**CSS GRid**

Grid is the latest in CSS for creating a layouts. 

You can follow [this](https://gitlab.com/barcelonacodeschool/css-grid-basics) workshop and please use (http://gridbyexample.com)


