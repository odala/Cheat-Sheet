# CSS for dummies

1. A CSS rule starts with a selector. A selector specifies which HTML elements to style.
Another available selector is the class selector.
2. Inside the braces `{ }`, a property and its value define what aspect of the `h1` elements to style.

Here the `h1` CSS selector selects all `h1` HTML elements on the page.
Setting the color property to red changes the color of the `h1` element to red.

``` css
h1 {
    color: red;
}
```

The `.header` selector applies a blue text color only to the elements nested inside `<div class="header">..</div>`

``` css
.header {
    color: red; /*red, rgb(102,153,0) or #9933CC*/
    font-family: Arial, Helvetica, sans-serif; /*"Times New Roman", Times, serif; or "Courier New", Courier, monospace; */
    font-size: 60px; /*pixels, ems, rems*/
    font-weight: bold;
    text-transform: uppercase;
    background-color: #0099cc;
    /*or*/
    background-image: url('http://goo.gl/ODpi3y');
    height: 500px;
    margin: 14px; /* creates space for multiple HTML elements. The margin is a transparent area outside the border of an element. Can be set on each side: margin-top/bottom/left/right. If -left or -right is set to auto then it will take as much as possible! (if margin-right: auto you get all elements to the left)*/
    padding: 23px; /*creates space between the content and border of an element. It's possible to set the padding on each side: padding-top/bottom/left/right*/
    border: 3px solid #cc0000;
}
```

This CSS selector selects any `p` element nested inside an HTML element with the class named `header`, and colors it blue. 

``` css
.header p {
  color: blue;
}
```

CSS treats HTML elements like boxes. A box can be "block" or "inline".

``` css
.nav li {
    display: block; /*Block elements display on a new line (e.g., h1, p, ul, li). Inline elements display on the same line as their neighboring elements (e.g., img, a)*/
    position: relative; /*relative/fixed. Use top, left, bottom, and right to shift an element away from where it would have normally appeared on the page*/
    float: right; /*moves an element to the far right(/left)*/
}
```

Bootstrap's grid is made up of 12 equal-sized columns. Each piece of content is aligned to this grid by specifying the number of columns to span.*/
/*check out: http://getbootstrap.com/css/*/
/*creates a horisontal group*/

``` css
<div class="row">

  <div class="col-md-6">    /*spans six columns*/
    <h4>Content 1</h4>
  </div>

  <div class="col-md-6">
    <h4>Content 2</h4>
  </div>

</div>
```

Creates tab navigation (or pill navigation by substituting nav-tabs with nav-pills)
``` css
<ul class="nav nav-tabs"> 
    <li><a href="#">Primary</a></li>
    <li class="active"><a href="#">Social</a></li>
    <li><a href="#">Promotions</a></li>
    <li><a href="#">Updates</a></li>
</ul>
```

jumbotron: large showcase area featuring important content
``` css
<div class="jumbotron">
    <h1>Find a place to stay.</h1>
    <p>Rent from people in over 34,000 cities and 192 countries.</p>
</div>
```






