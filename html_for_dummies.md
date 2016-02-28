# HTML 5 for dummies

## General structure of a .html-file
Everything inside the body will be presented on the website.
``` html
<<!DOCTYPE html>
<html>
  <head>
    <title></title>
  </head>
  
  <body>

  </body>
</html>
```

## Heading
``` html
<h1>This is the main heading</h1>
```

## Paragraph
``` html
<p>This is a paragraph.</p>
```

## Link to a page
``` html
<a href="https://www.google.com/">This is a link to Google.</a>
```

## Add an image
``` html
<img src="http://goo.gl/mbnqBl">
```

## A bulleted list
A bulleted list is described using a ul element. Each item in the list is placed inside an li element.
``` html
<ul>
  <li>Brand</li>
  <li>Browse</li>
</ul>
```

## Include JavaScript-files
Place within `<body> </body>`
``` html
<script src="jquery.min.js"></script>
<script src="app.js"></script>
```

## Include .css-files
Place within `<head> </head>`
``` html
<link href="font.css" rel="stylesheet"> <!-- Order matters! First, make fonts available to the webpage, then use it in the main.css-->
<link href="main.css"rel="stylesheet"/>
```

## Group elements together
A `<div>` element groups other elements together into sections of the web page, such as a navigation bar, the main body, and the footer.
``` html
<div class="xxx"> <!-- "nav": groups the elements into the navigation bar section. "jombotron":groups the elements into the large feature section of the web page.-->
    <div class="container"> <!--  wraps the contents in a container-->
    </div>
</div>
```

