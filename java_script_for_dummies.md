# JavaScript for Dummies

``` javascript
var main = function() {
    
};
```

`$(document).ready(main);`

`$()` selects existing HTML elements on the page.
`$('p')` selects all `p` elements on the page
`$('.article h2')` selects all `h2` elements nested inside the `<div class='article'></div>`
`$('<h1>')` creates a new `h1` element.

* `.text()` adds text to the the selected element.
  * with `.appendTo('.items')` is it added to the end of an HTML element.
  * with `.prependTo()` is it added to the beginning

* `.remove()` remove the selected HTML element
* `.hide()` hides the selected HTML element
* `.show()` displays an element
* `.toggle()` alternates hiding and showing an element
* `.addClass()` adds a CSS class to an element
* `.removeClass()` removes a class from an element
* `.toggleClass()` alternates adding and removing a class from an element

## Document Object Model (DOM):
* `.next()` gets the next sibling of the selected element.
* `.prev()` gets the previous sibling of the selected element.
* `.children()` gets the children of the selected element. If given a selector a spesific child can be selected.
