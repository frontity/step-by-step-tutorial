# Use the `<Link>` component

> *__[TO DO]__ modify this text to suit new context.*

> *__[TO DO]__ adapt to use new Link component. ✅*

> *__[TO DO]__ This step will explain how to use components from `frontity/components` and how you can work with links in a frontity project
Will also point out that pre-fetching strategies can be applied with this component (link to further explanations)*

Now that we've seen how `state.router.link` stores the current URL, let's create a navigation to change the URL.

Frontity provides a `<Link>` component. The simplest way to use it is to just provide a `link` attribute with the URL as it's value:

```jsx
<Link link="/">Home</Link>
```

We also provide the string that we want to be displayed as a clickable link. In the example above that is 'Home'.

Before we can use the `<Link>` component we first need to import it into our `Root` component. Add this as the third line:

```jsx
import Link from "@frontity/components/link";
```

We are now in a position to add a menu consisting of a `<nav>` element with three `<Link>` items as children. Your `index.js` file should now look like this:


```jsx
// File: /packages/my-first-theme/src/components/index.js

import React from "react";
import { connect } from "frontity"
import Link from "@frontity/components/link";

const Root = ({ state }) => {
  return (
    <>
      <h1>Hello Frontity</h1>
      <p>Current URL: {state.router.link}</p>
      <nav>
        <Link link="/">Home</Link><br />
        <Link link="/page/2">More posts</Link><br />
        <Link link="/about-us">About Us</Link>
      </nav>
    </>
  );
};

export default connect(Root);
```

> Here we've used the `<Link>` component in the simplest possible way. To learn more about what you can do with the `<Link>` component [see this page](https://docs.frontity.org/api-reference-1/frontity-components#link) in our documentation.