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

TODO
