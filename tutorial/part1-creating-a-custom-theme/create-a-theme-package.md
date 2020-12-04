# Create a Theme Package

As stated previously, rather than using the default starter theme that we selected during the setup process (i.e.@frontity/mars-theme) we are instead going to develop a custom theme from scratch. To do this we need to create a new package for our theme's code. As it's our first ever theme let's call our theme "my-first-theme".

> **NOTE:** Before continuing you may need to stop the previous process with _CONTROL+C_.

To create a package run the following command in the terminal:

```bash
> npx frontity create-package my-first-theme
```

You will be prompted to specify the namespace to use. Since you are creating a theme you can use the default `theme`, so you can just press _Enter_ at this point.

<p>
  <img alt="Creating a package" src="../assets/part1img2.png">
</p>

When the process is complete you will have a new folder called `/packages/my-first-theme`. This is where we will be doing most of our work to build the theme.

<p>
  <img alt="Structure of a newly created package" src="../assets/part1img3.png">
</p>

The first thing we'll do is to remove `@frontity/mars-theme` from our settings and replace it with `my-first-theme`.

Remove the following from the file `frontity.settings.js`:

```js
// File: /frontity.settings.js

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
// File: /frontity.settings.js

{
  name: "my-first-theme"
},
```

We've now told Frontity to use our new theme rather than "mars-theme". Save the file and then run this command again:

```bash
> npx frontity dev
```

You will see this in your browser:

<p>
  <img alt="Frontity in the browser" src="../assets/part1img4.png">
</p>
