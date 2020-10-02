# Frontity step-by-step tutorial

## Welcome to the Frontity step-by-step tutorial

> *__[TO DO]__ Explain what we'll build in the tutorial and more or less the topics that will be covered in the tutorial.*

> *__[TO DO]__ Brief explanation of Frontity - React-based framework for building themes for headless/decoupled WordPress.*

Explain what we'll build in the tutorial and more or less the topics that will be covered in the tutorial.

Brief explanation of Frontity - React-based framework for building themes for headless/decoupled WordPress.

We'll be building a blog site

We'll create a custom theme from scratch
 - learn about Frontity state, actions and source
 - create a list component
 - create components for pages and posts
 - navigation/menu
 - styling - CSS in JS
 - custom post types
 - SEO and head tags
 - deploying the finished site

----

- 0. **Building a Blog with Frontity**

    *Explaing what we'l build in the tutorial and more or less the topic that will be covered in the tutorial*

- 1. **Creating a custom theme**
    - Start a Frontity Project

        *This step will show the use of `npx frontity create` and a brief explanation of the structure*

    - Create a custom theme

        *This step will show how to create a package (theme) and a brief explanation of the structure of a package*

    - Modify the `<Root>` component
    - Connect the `<Root>` component to the state

        *This step will explain `connect` and how it's used to pass the Frontity state to the React components via props*

- 2. **Adding a menu**
    - Using new Link component *(differs from original in JS Nation workshop)*

        *This step will explain how to use components from ``frontity/components`` and how you can work with links in a frontity project
        Will also point out that pre-fetching strategies can be applied with this component (link to further explanations)*

- 3. **Displaying posts**
    - Understanding the Frontity `state` - using data from the current URL → The “two-step” access to data
    - Display the list of posts → The “two-step” access to data
    - Display the post content → The “two-step” access to data
    - Display posts and pages separately
        - Make use of `isPost` of  `isPage`  (Frontity Magic in action!)
        - Different component for different content type (Custom component creation)
- 4. **Adding styling**
    - Add styling
    - Add dynamic styling
- 5. **Adding behavior**
    - Use `state` and `actions`
    - Add pagination
- 6. **Custom Post Types**
    - Add support for custom post types in`frontity.settings.js`
    - Add 10 best travel destinations page
    - Create a custom component for showing individual CPT's
- 7. **Taking care of the SEO**
    - Add tags to the `head` element
- 8. **Deploying the project**
    - Deploy to Vercel
- 9. **Next Steps**
    - Guide to the documentation
    - Getting help and support (community forum)
    - Contributing to Frontity

