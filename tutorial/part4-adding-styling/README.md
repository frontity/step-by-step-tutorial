# Adding styling

Awesome, we now have a fully functioning website! But you're probably looking at it and thinking "I've seen prettier warthogs!" 🐗

Let's fix that in this section. This is where we'll take a look at styling our components.

Frontity uses [Emotion](https://emotion.sh/docs/introduction), a CSS-in-JS library, for styling components. This has a number of advantages:

- it only loads the CSS needed for each page which improves the performance
- you don't have to worry about classes and problems with duplication, typos, etc
- you don't have to worry about vendor prefixing so you can write your CSS based on the current standard and Frontity handles the rest for you
- you can use all the power of JavaScript to style your components and create dynamic styles with ease

In this section we'll look at the `<Global>` component which enables you to apply styles site wide, and at the `styled` function which enables you to create styled components for use within the components that we've already created.

We'll then go on to look at how we can use styled components to apply styling to components we've already imported and used, such as the `<Link>` component, and finish off this section by looking at dynamic styling.

Dynamic styling is styling that is applied conditionally and is one of the great advantages of the CSS-in-JS approach.

Without further ado let's start making our site look good! 🎨

{% hint style="info" %}
We'll get you started with some CSS-in-JS basics here, but you can learn more about styling your Frontity app [in our docs](https://docs.frontity.org/learning-frontity/styles).
{% endhint %}
