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
- Add commas for the last item in a list to allow easy additions to the list in future revisions.

    ```
    # good
    l = [
        'hello',
        'world',
    ]
    
    # bad
    l = [
        'hello',
        'world'
    ]
    ```

## HTML

- Use double quotes for attribute values, `<a href="http://google.com">`
- We tend to use classes over ids, even if it's only to identify one element on the page. Possibly aesthetic so that CSS and Javascript can use `.my-class` instead of `#my-id`.
- Name classes with hyphens. `class="my-class"` instead of `class="my_class"` or `class="myClass"`
- Use `<button>` over `<input type="button">`

## CSS/Sass

- Double quotes for any values requiring quotes
- Avoid using color names if possible, using hex codes instead, due to differing cross browser implementations of each color. Possible exceptions include white, black, or red, but avoid using these also if possible. Even better, define Sass variables for hexes and use those
- Use hyphens for Sass variables and mixins

## Javascript

- Use double quotes instead of single quotes
- Use `camelCase` for variables and function names, except use `UNDERSCORE_CAPS` for variables that should be considered constants
- Use the following format to declare and document a function:

    ```
    /**
     * A short description of the function
     * 
     * @param {type} x -- description of this parameter
     * @return {type} description of the return value
     */
    var myFunction = function(x) {
        // stuff
    };
    ```

## C++

### Code Formatting and Naming Conventions

Refer to the [WebKit Code Style Guidelines](https://webkit.org/code-style-guidelines/).

Please pay particular attention to the naming conventions; indentation and other formatting will generally be applied automatically using the `clang-format` program. 

### Use `const`

If a method, when applied on an object, makes no changes to that object, then it should be declared as `const`.

Example:
```
class IntWrapper {
public:
    IntWrapper(int x): m_x(x) {}; // Constructor
    
    // Getter method: declared const because it does not modify the object
    // Note that the `const` keyword follows the 
    int getX() const {
        return m_x;
    }
private:
    int m_x;
};
```

If a mutable object is passed as an argument to a function/method that does not make any changes to it, then the parameter should be declared as `const`.

Example:
```
void funcA(const int& readonly) {
    print(readonly); // Note that we do not change the value of readonly, so we declare it const
}

void funcB(int& readWrite) {
    readWrite++; // Note that we are editing the value of readWrite, so we cannot declare it const
    print(readWrite); 
}
```

### Smart Pointers

Avoid raw pointer types (e.g. `int*`); instead, use smart pointers. There are three types, and all can be accessed by including `<memory>`. The three types are introduced briefly below; it is recommended that you supplement the material below with other online resources.

#### `std::unique_ptr`

Unique pointers will delete the objects which they point to when they are deleted or go out of scope. Consider the following function, which uses a raw pointer instead of a unique pointer:

```
void func() {
    SomeClass* something = new SomeClass();
    doSomething(something);
    something->someMethod();
    delete something; // We allocated memory for 'something'; we need to free it before we leave
}
```

Note that if we forget to explicitly call `delete`, we will create a memory leak. Also note another issue: suppose that `doSomething(something)` aborts after throwing an exception; in that case, `func()` will not finish executing, and `delete something` will never be executed, causing a memory leak. To avoid both of these problems, we can rewrite the function with a unique pointer:

```
void func() {
    std::unique_ptr<SomeClass> something(new SomeClass()); // Note that `std::unique_ptr` is a template, so you must specify the type of pointer in the angle brackets (<SomeClass>)
    doSomething(something.get()); // We can extract the raw pointer from our unique pointer using `get()`, so we can still use the `doSomething` function
    something->someMethod(); // Note that we can still use the `->` operator to call `someMethod`, just as before
}
```

Note that if the call to `doSomething(something.get())` aborts with an exception, then `something` will go out of scope, and will thus safely delete the object that it points to. Also note that if the call to `func()` completes successfully, `something` will also go out of scope, and the object that it points to will be deleted without an explicit call to `delete`.

#### `std::shared_ptr`

Unique pointers will automatically delete the object that they point to as soon as they go out of scope. For this reason, different unique pointers cannot address the same object, since they will all attempt to delete that same object when they go out of scope. To avoid this issue, use shared pointers. An object can be addressed by many shared pointers, and will only be deleted once all of those shared pointers have been deleted or have gone out of scope.

Example:
```
void func() {
    std::shared_ptr<SomeClass> ptr1 = std::make_shared<SomeClass>();
    std::shared_ptr<SomeClass> ptr2 = ptr1;
    doSomething(ptr1.get());
}
```

Note that we have two pointers to the same object, but the object is not deleted until both of these pointers go out of scope, so it is only deleted once (this would not be the case with `unique_ptr`).

#### `std::weak_ptr`

Suppose you have objects which have pointers to each other. Specifically, suppose you have objects `a` and `b`, and that each of them have a pointer attribute called `ptr`. Then the following function would cause a circular reference:

```
a->ptr = b;
b->ptr = a;
```

Even all other pointers to `a` and `b` are deleted or go out of scope, `a` will still have a pointer to `b` and `b` will still have a pointer to `a`. If `ptr` is a shared pointer, then `a` will not be deleted until `b`'s shared pointer is deleted, and `b` will not be deleted until `a`'s shared pointer is deleted. Consequently, the two objects will keep each other alive even after they are forgotten by the rest of the program, causing a memory leak. To solve this, we can use weak pointers. 

Unlike a shared pointer, the existence of a weak pointer will not prevent the object that it addresses from being deleted. A single object may be safely addressed by a combination of many shared pointers and many weak pointers. 

To use the object addressed by a weak pointer, you must activate the weak pointer using the `lock()` method. This will create a temporary shared pointer that will give you access to the addressed object and will keep the it alive until you are finished with it.

### Pointers vs. References

Whenever possible, prefer a reference to a pointer. A pointer is required under the following circumstances:

- A pointer must be used if the value can be null (`nullptr`)
- A pointer must be used if the address that is pointed to can be changed
