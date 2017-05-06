#Bootstrap CDNs
```
CSS:
https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css

JS:
https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js
```
Source: [BootstrapCDN](https://www.bootstrapcdn.com/)

Literally everything in this post is learned from the basic page [here](http://getbootstrap.com/examples/grid/). I recommend viewing the page and its source here first if you've never learned it before, and coming back to the remaining content of this page as a refresher. Nothing is better than the visual examples at the link above. 

The actual CSS documentation page goes into more detail [here](http://getbootstrap.com/css/#grid-responsive-resets).

#Basic HTML Page
```
<html lang="en">
    <head>
        <meta charset="utf-8">

        <title> Hello, World! </title>
    </head>
    <body>
        <div class="container">
            <div class="row">
                <div class="col-md-4">.col-md-4</div>
                <div class="col-md-4">.col-md-4</div>
                <div class="col-md-4">.col-md-4</div>
            </div>
        </div>
    </body>
</html>
```

### The Bare, Bare Minimum
Have the overarching parent container have the class `container`.

### The Grid System
Each row starts by having a class of `row`. The elements within this `div` should have classes in the format of:
```
col-<screen size>-<weight>
```

where the screen size is of four possible sizes:
```
xs (phones), sm (tablets), md (desktops), and lg (larger desktops)
```

and the `weight` value could be anything from 1 to 12 - the caveat being that the elements at each row must have a sum of 12. 

Nested columns are possible + allows for two columns starting at the `desktop (md)` level and scaling to `large desktops (lg)` with another two equal widths within the larger column.

Each tier of classes scales up, so setting the same widths for xs and sm only requires setting the width for xs.

**Spacing**

Within the 12 point weight system is the ability to do spacing. It's possible to have a row with a combo of content and space like:
```
[ CONTENT HERE ]  [ SPACING ]  [ MORE CONTENT HERE ]  
   <col-md-5>  <col-md-offset-2>    <col-md-5>
```

As you can see, the naming for the offset is described in the example above.

**Clearing**

This is the most obscure to me. Clear floats at a desired breakpoint to help with wrapping content unevenly. 

```
   <div class="clearfix visible-xs"></div>
```

**Centering Content/Text**

Use the `mx-auto` class for `display:block` and `row` delements.

Use `text-center` for `display:inline` and text elements.

See an example [here](http://www.codeply.com/go/SOSvvKpLOc) and checkout a useful SO post [here](http://stackoverflow.com/questions/18153234/center-a-column-using-twitter-bootstrap-3)