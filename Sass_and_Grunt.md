# Sass and Grunt

Instead of using CSS files, we usually use [Sass](http://sass-lang.com) that allows additional features on top of what CSS offers. Some features Sass has include:

- Variables

    ```scss
    $base-color: #10a4da;
    p {
        color: $base-color;
    }
    div {
        background-color: $base-color;
    }
    ```
    
    Will render to:
    
    ```css
    p {
        color: #10a4da;
    }
    div {
        background-color: #10a4da;
    }
    ```

- Nested selectors

    ```scss
    p {
        font-size: 18px;
    }
    div {
        margin: 10px;
        &.blue-text {
            color: blue;
        }
        p {
            font-weight: bold;
        }
    }
    ```

    Will render to:

    ```css
    p {
        font-size: 18px;
    }
    div {
        margin: 10px;
    }
    div.blue-text {
        color: blue;
    }
    div p {
        font-weight: bold;
    }
    ```

- Mixins

    ```scss
    @mixin berkeley_palette {
        color: blue;
        background: yellow;
        &:hover {
            color: yellow;
            background: blue;
        }
    }

    p, div, h1 {
        @include berkeley_palette;
    }
    ```
    
    Will render to:
    
    ```css
    p, div, h1 {
        color: blue;
        background: yellow;
    }
    p:hover, div:hover, h1:hover {
        color: yellow;
        background: blue;
    }
    ```

We save our Sass files using the `.scss` extension (the `.sass` extension has a different syntax, and we just use the SCSS syntax). To compile Sass files into CSS files, we use a package called [Grunt](http://gruntjs.com).

Grunt allows us to specify tasks we want it to do. We typically take advantage of Grunt's `build` and `watch` commands.

- `grunt build` compiles all of the Sass files into CSS files
- `grunt watch` watches for changes to Sass files, when it will automatically compile the changed file into CSS

Most projects with Grunt include a `vgrunt.py` script, which is the same thing as running `grunt`, except it [runs in the VM](https://github.com/calband/compcomm-info/blob/master/Vagrant.md) instead of running locally, so you don't have to install Grunt on your computer. Run with `python vgrunt.py <command>`.
