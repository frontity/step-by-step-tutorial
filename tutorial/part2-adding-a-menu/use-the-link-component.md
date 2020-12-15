# Use the `<Link>` component

In the last lesson we saw that `state.router.link` stores the current URL. We demonstrated this by manually changing the URL in the browser's address bar. In this lesson we will create a menu-based navigation to change the URL for us.

Frontity provides a `<Link>` component. The simplest way to use it is to just provide a `link` attribute with the URL as it's value:

```jsx
<Link link="/">Home</Link>
```

We also provide the string that we want to be displayed as a clickable link. In the example above that is 'Home'.

Before we can use any of Frontity's built-in components we first need to import it. Frontity's built-in components are imported from `@frontity/components`.

So let's import the `<Link>` component into our root component file for use within our `<Root>` component. Let's add this import statement as the third line:

```jsx
import Link from "@frontity/components/link"
```

With that done we are now in a position to add a menu consisting of a `<nav>` element with three `<Link>` items as children. Using the example above as a template our `index.js` file can now look like this:

```jsx
// File: /packages/my-first-theme/src/components/index.js

import React from "react"
import { connect } from "frontity"
import Link from "@frontity/components/link"

const Root = ({ state }) => {
  return (
    <>
      <h1>Hello Frontity</h1>
      <p>Current URL: {state.router.link}</p>
      <nav>
        <Link link="/">Home</Link>
        <br />
        <Link link="/page/2">More posts</Link>
        <br />
        <Link link="/about-us">About Us</Link>
      </nav>
    </>
  )
}

export default connect(Root)
```

When you save the file the browser should update and the menu will now be visible. Now if you click on the menu items you will see the URL in the browser's address bar change, and also the displayed value of `state.router.link`.

{% hint style="info" %}
Here we've used the `<Link>` component in the simplest possible way. To learn more about what you can do with the `<Link>` component, including pre-fetching strategies to make your site more responsive, [see this page](https://docs.frontity.org/api-reference-1/frontity-components#link) in our documentation.
{% endhint %}
