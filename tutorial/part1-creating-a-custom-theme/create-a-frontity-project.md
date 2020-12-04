# Create a Frontity Project

The first thing we are going to do is create a new Frontity project. As it's our first time exploring Frontity we will call our project `hello-frontity`.

To create the project, open up your terminal, navigate to the folder where you want to install your new project, and run this command:

```bash
> npx frontity create hello-frontity
```

Select the `mars-theme` - it's the basic starter theme that we recommend for beginners.

> We won't be using `mars-theme`, we will instead be using the custom theme that we will build over the course of this tutorial, but you need to select a theme during the setup process.

When the install process finishes, you will have a new sub-folder called `hello-frontity` containing your project’s code. The structure of the project should look like this:

<p>
  <img alt="Frontity project structure" src="../assets/part1img1.png">
</p>

Let's take a look at the file `frontity.settings.js`. This is the configuration file for our project. One of the elements that you'll see here is an array of `packages`. In Frontity everything is a package, including the theme, so one of the packages in the array is `@frontity/mars-theme`. We'll be replacing this in the next lesson.

Another package in the array is `@frontity/wp-source`. This has a property: `state.source.url`. This is where you define the WordPress site that you want to connect to in order to get data from the REST API. Changing this is one of the first things you would normally do when configuring a Frontity project, but let's leave this as it is as this is the data that we are going to be working with during this tutorial.

```js
// File: /frontity.settings.js

// ...
{
  name: "@frontity/wp-source",
  state: {
    source: {
      url: "https://test.frontity.org",
    },
  },
}
```

Now that we have our Frontity project set up and we've had a good old poke around to see how it's structured and configured let's test that everything is working.

Change directory into the project folder and start a development server:

```bash
> cd hello-frontity
> npx frontity dev
```

> `npx` downloads an npm package to run just this one time and then removes it from your computer. [learn more here](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b).

A new browser tab should open automatically for you. If it didn't then open `http://localhost:3000` in your browser. You should now see your first Frontity project. At the moment it's using the "starter theme" that we selected earlier, i.e. `@frontity/mars-theme`, and it is connected to our test WordPress site (i.e. https://test.frontity.org as defined in `frontity.settings.js` at `state.source.url`) which you will see contains a travel blog as its content.

In the next step we'll start creating our own Frontity theme.
