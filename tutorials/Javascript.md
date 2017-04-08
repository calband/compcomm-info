Javascript
==========

This is a very brief introduction to Javascript. I will first be going over the basic syntax of Javascript, and then talk about how to use Javascript in a webpage using jQuery.

## Syntax

Javascript is most similar to Python: it is dynamically typed and is functional (i.e. functions are objects that you can manipulate and pass around). Here are some basic syntax expressions:

```js
// assign 1 to the variable x
var x = 1;

// assign "hello world" to the variable y
var y = "hello world";

// reassigning a declared variable
x = 2;
x = 1 + 2;
x += 3; // x = x + 3
x++; // increment x

// if-statement
if (x < 5) {
    y = "low";
} else if (x < 10) {
    y = "medium";
} else {
    y = "high";
}

// use triple equals in Javascript for more correct code
x === 5;

// print to the console
console.log(y);

// arrays
var a = [1, 2, 3];
console.log(a[0]); // 1
a.length; // 3

// while loop
var z = 1;
while (z < 10) {
    console.log(z);
    z++;
}

// for loop
for (var i = 0; i < 10; i++) {
    console.log(i);
}
```

The console is opened differently by browser:

- Chrome: View > Developer > JavaScript Console
- Firefox: Tools > Web Developer > Web Console
- Safari: Develop > Show JavaScript Console

### Scope

Unlike in Java, variables in Javascript are not block-scoped; they are scoped by function. For example:

```js
function foo() {
    var x = 1;
    if (x > 4) {
        var y = 1;
    } else {
        var y = 2;
    }
    // y exists
}
// x does not exist
```

### Functions

Functions can be declared in two ways:

```js
function foo(x) {
    return x + 1;
}

var bar = function(x) {
    return x - 1;
};

foo(1); // 2
bar(2); // 1
```

In the first, `foo` is declared as a function in the form you're probably used to. The second creates a variable `bar` that is assigned an anonymous function. In the end, both are used the same way, and the difference is [technical](https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/).

### Objects

Just like how Python offers dictionaries, Javascript offers objects.

```js
var o = {
    a: 1,
    b: 2,
};

o["a"]; // 1
o["b"]; // 2
o["c"]; // undefined
```

Note that retrieving a non-existent key returns undefined; Javascript doesn't throw a lot of errors (intentionally). Objects can also be indexed using dot-notation:

```js
o.a; // 1
o.b; // 2
o.c; // undefined
```

Why is this important? Because in Javascript, **everything is an object**! Like, pretty much everything.

```js
var foo = function() {
    return 1;
};

foo.a = 2;
console.log(foo.a); // 2
console.log(foo()); // 1

foo.bar = function() {
    return 3;
};
console.log(foo.bar()); // 3
```

As you can imagine, this is exactly how "classes" work in Javascript. I put that in quotes, because there aren't really classes in Javascript. But the way they work is effectively:

```js
var bob = {
    firstName: "Bob",
    lastName: "Calonico",
    eat: function(food) {
        return "Ate " + food;
    },
};
bob.firstName; // "Bob"
bob["lastName"]; // "Calonico"
bob.eat("apple"); // "Ate apple"
```

### Classes

As mentioned in the Objects section, there aren't really classes in Javascript; Javascript uses what are called "prototypes". You don't need to know too much about this system, but here is an OOP example:

```js
var Person = function(first, last) {
    this.firstName = first;
    this.lastName = last;
};

Person.prototype.changeFirst(newFirst) {
    this.firstName = newFirst;
}

var bob = new Person("Bob", "Calonico");
bob.firstName; // "Bob"

bob.changeFirst("Robert");
bob.firstName; // "Robert"

// again, bob is still an object
bob["lastName"]; // "Calonico"
```

## Web Development

It is possible to do some web development with pure Javascript, but using the jQuery library makes life so much easier. When you include the jQuery library in the `<head>` section, you can now use the `$()` function in your code. This function gives you a jQuery object, which wraps HTML nodes. You can either initialize a jQuery object with a jQuery selector (CSS selectors work here) or by passing in an HTML node.

```js
// a jQuery object containing all <p> elements
$("p");
// number of elements in the object
$("p").length;

// jQuery object containing all elements with class "foo"
$(".foo");

// indexing gives you the HTML node
var node = $("#foo")[0];
$(node); // jQuery object re-wrapping the HTML node
```

Using jQuery, you can traverse the HTML in a page:

```js
var body = $("body");
body.children(); // all direct children of <body>

var child1 = body.children().first(); // first child of <body>
var child2 = child1.next(); // next sibling of child1; i.e. second child of <body>
child1 === child2.prev(); // previous sibling of child2; i.e. back to child1
child1.siblings(); // all siblings of child1; i.e. all children of <body> except child1

child1.find("p"); // all <p> elements that are descendants of child1
child1.children("p"); // all <p> elements that are direct children of child1
```

jQuery also provides functions that manipulate all wrapped HTML nodes:

```js
// add class "foo" to all <p> elements
$("p").addClass("foo");

// set the text of all <span> elements with the class "hello"
$("span.hello").text("Hello world!");

// set the CSS for all <div> elements, two ways to do it
$("div").css("height", 10);
$("div").css({
    background: "red",
    margin: 10,
    width: "100%",
});

// iterate through each <p> element
$("p").each(function() {
    this; // the current <p> HTML node
    $(this); // wrap in jQuery object to do jQuery functions
});
```

Most functions in jQuery return a jQuery object, so you can chain calls together:

```js
// does the following on all <p> elements
$("p")
    .addClass("foo bar")
    .css("background", "red")
    .text("Hello world!");
```

One powerful technique in jQuery is using event listeners.

```js
// listen for a click on any <p> element
$("p").on("click", function(e) {
    this; // the element that was clicked
    e; // the Event object, see jQuery API
});

// trigger a click event on the selected <p> elements
$("p.my-class").trigger("click");

// short for .on("click", function)
$("p").click(function(e) {
    ...
});
// short for .trigger("click")
$("p").click();

// listen for when user hovers over element
$("p").hover(...);
// listen for when user types in the element
$("input").keydown(...);
$("input").keyup(...);
// listen for when user changes the value
$("select").change(...);
```

You can run all these commands in the console and watch the effects on the page, but in a script, you need to do something special, because when the script is run, there won't be any elements on the screen yet:

```html
<html>
    <head>
        <script src="jquery.js"></script>
        <script>
            // at this point, there are no <p> tags loaded yet!
            $("p").addClass("foo");
        </script>
    </head>
    <body>
        <p>Hello world!</p>
    </body>
</html>
```

So in your code, you'll need to wrap any HTML manipulation code in a callback that will be run when the page is loaded:

```js
$(document).ready(function() {
    // will be run when page is loaded
    $("p").addClass("foo");
});

// the currently recommended way, same as above
$(function() {
    $("p").addClass("foo");
});
```

The [jQuery API](http://api.jquery.com/) is really helpful, and you should definitely reference it a lot!
