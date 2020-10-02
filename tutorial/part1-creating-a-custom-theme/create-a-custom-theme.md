# Create a custom theme

> **[TO DO]** modify this text to suit new context.

> **[TO DO]** add a brief explanation of the structure of a package.

Instead of using the default starter theme (@frontity/mars-theme) we are going to create a new package for our theme's code.

To do so, stop the previous process (CONTROL + C), and then run this command in your terminal:

```bash
npx frontity create-package jsnation-theme
```

You will be asked what namespace to use. Since you are creating a theme, you can use `theme`.

When the process is complete you will have a new folder called `/packages/jsnation-theme`. This is where we will be doing most of our work to build the theme.

The first thing to do is to remove `@frontity/mars-theme` from your settings and replace it with `jsnation-theme`.

Remove the following from the file `frontity.settings.js`:

```js
{
  name: "@frontity/mars-theme",
  state: {
    theme: {
      menu: [
        ["Home", "/"],
        ["Nature", "/category/nature/"],
        ["Travel", "/category/travel/"],
        ["Japan", "/tag/japan/"],
        ["About Us", "/about-us/"]
      ],
      featured: {
        showOnList: false,
        showOnPost: false
      }
    }
  }
},
```

And replace it with:

```js
{
  "name": "jsnation-theme"
},
```

Save the file and then, run this command again:

```bash
npx frontity dev
```

You will see this in your browser:

<p>
  <img alt="Frontity in the console" src="../assets/browser-1.png" width="400">
</p>