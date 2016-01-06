# General Comp-Comm Style

This file will list a few languages we use in our projects and some stylistic guidelines for each language.

## General

- End each file with a newline. This makes things easy on Unix systems, Github won't complain, and it keeps files consistent.

## Python

Use the following style conventions for coding style and formatting. Extensive python style documentation available at [PEP 8](https://www.python.org/dev/peps/pep-0008/).

- Indent with 4 spaces, not tabs.
- Use `snake_case` for functions and variables, `CapitalCamelCase` for classes
- Use the following format for documentation:

    ```
    def some_function(param1, param2):
        """
        Have some overall description of what this function does here, including
        descriptions of the parameters and what is returned
        """
        # do stuff

    def other_function(self):
        """Short description of this mostly intuitive function"""
        # do stuff

    ```

    Try to write docs as a command, instead of a description. For example, "Take a list and return something" instead of "Takes a list and returns something".
- Avoid using wildcard imports (`from module import *`) because they can be ambiguous (if there are wildcard imports, then it's sometimes not clear where exactly a function that's imported as part of the `*` is defined, which means you can't look it up).
- Use single quotes for strings instead of double quotes, unless you want single quotes inside the string. This is purely arbitrary, and simply for consistency.

    ```
    'hi'
    "It's an apostrophe"
    'She said, "Hi!"'
    ```
- Use string interpolation instead of string concatenation. It's cleaner, checks for type, and is supposed to be faster.

    ```
    # good
    s = 'Hello %s! You are user #%d' % (name, id)
    # bad
    s = 'Hello ' + name + '! You are user #' + id
    ```

## HTML

- Use double quotes for attribute values, `<a href="http://google.com">`
- We tend to use classes over ids, even if it's only to identify one element on the page. Possibly aesthetic so that CSS and Javascript can use `.my-class` instead of `#my-id`.
- Use `<button>` over `<input type="button">`

## CSS/SASS

- Double quotes for any values requiring quotes
- Avoid using color names if possible, using hex codes instead, due to differing cross browser implementations of each color. Possible exceptions include white, black, or red, but avoid using these also if possible.

## Javascript

- Use double quotes instead of single quotes
- Use `camelCase` for variables and function names, except use `UNDERSCORE_CAPS` for variables that should be considered constants
- Use the following format to declare and document a function:

    ```
    /**
     * A short description of the function
     * 
     * @param (type) x -- description of this parameter
     * @return (type) description of the return value
     */
    var myFunction = function(x) {
        // stuff
    };
    ```

## C++
