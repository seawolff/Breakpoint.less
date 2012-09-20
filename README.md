#Breakpoint.less
##Dynamic breakpoint classes controlled solely in LESS

Add breakpoint-specific classes simply by including a less file.

##Why LESS? Why not JavaScript?

Breakpoint.less simply removes the need to detect viewport changes in Javascript. Instead it simply passes a classname to the body for each defined breakpoint in the stylesheet.

##So why is this useful?

This is simply another way of dynamically customizing your responsive interface. Instead of having to check viewport width via JavaScript, Breakpoint.less will update the body with a custom class based on the viewports current breakpoint.

From here the developer can manipulate form elements etc. as needed in order to optimize the DOM for the current viewport width.

##How it works...
Breakpoint.less simply gives the body a content property at specified breakpoints. An example:

    @media(min-width:768px) {
      body#main {
        content:"seven-sixty-eight";
      }
    }

From there it simply executes two lines of JavaScript that check onload and on window resize whether that computed style has changed. From there it appends it to the class of the body. Dead simple.

    body#main{
      content: `window.onload = function() {
                  document.getElementById('main').className = window.getComputedStyle(
                    document.getElementById('main'),':before').content
                }`;
      content: `window.onresize = function() {
                  document.getElementById('main').className = window.getComputedStyle(
                      document.getElementById('main'),':before').content
                }`;
    }

To add a new body class one could simply add another content property to the body class at any specified breakpoint. However by default Breakpoint.less supports the following media queries: `max-width:480px`, `min-width:480px`, `min-width:768px`, `min-width:960px`, `min-width:1280px`, `min-width:1920px`

To add this functionality simply include the import at the top of your LESS stylesheet: `@import "breakpoint";`

##[Check out a live demo](http://seawolff.github.com/Breakpoint.less/)
