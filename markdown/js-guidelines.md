Make sure the content and main functionality on a web page on telia.se is accessible and usable without javascript. By using class=“no-js” on the HTML element, styling with css can be used to target user experiences when javascript is not present.

Don’t forget that every user is without javascript until the scripts have loaded. What may be seen in a browser until the scripts have loaded and started changing the page is important, especially in a mobile context where the loading of scripts to the page can be significantly delayed due to low network speed.

In order to keep initial markup as small as possible, and also to make javascript widgets as self-contained as possible, you should always let a javascript function add any additional markup needed for the actual function. Don’t clutter the markup with elements that are only intended for javascript functions.

Use jQuery as a library for developing javascript based functionality and widgets.


## jQuery


The chosen javascript library for developing functions and widgets is jQuery.


## Modernizr


To test a browser’s capabilities, we use Modernizr (http://modernizr.com) on telia.se. Modernizr adds classes to the <html> element, and these classes can be used to optimize the user experience according to a certain browser’s capabilities.


You can use .cssgradients … { … } to add styles for browsers that support css gradients, and .no-cssgradients … { … } for browsers that lack the support for css gradients.
Modernizr also creates a javascript object that can be used to test for capabilities using javascript, and depending on what the browser support, you can fire appropriate code.