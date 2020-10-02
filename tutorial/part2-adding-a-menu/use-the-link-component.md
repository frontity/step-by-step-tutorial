# Use the `<Link>` component

> *__[TO DO]__ modify this text to suit new context.*

> *__[TO DO]__ adapt to use new Link component.*

> *__[TO DO]__ This step will explain how to use components from `frontity/components` and how you can work with links in a frontity project
Will also point out that pre-fetching strategies can be applied with this component (link to further explanations)*

Now let's create a `<Link>` component in a new file `link.js`:

```jsx
// File: /packages/jsnation-theme/src/theme-files/link.js

import React from "react";
import { connect } from "frontity";

const Link = ({ href, actions, children }) => {
  return (
    <div>
      <a
        href={href}
        onClick={ e => {
          e.preventDefault();
          actions.router.set(href);
        }}
      >
        {children}
      </a>
    </div>
  );
};

export default connect(Link);
```

We now have to import the `Link` component into our `Root` component. Then we add a menu with three `Link` items.


```jsx
// File: /packages/jsnation-theme/src/theme-files/index.js

import React from "react";
import { connect } from "frontity";
import Link from "./link";

const Root = ({ state }) => {
  return (
    <>
      <h1>Frontity Workshop</h1>
      <p>Current URL: {state.router.link}</p>
      <nav>
        <Link href="/">Home</Link>
        <Link href="/page/2">More posts</Link>
        <Link href="/lorem-ipsum">Lorem Ipsum</Link>
      </nav>
    </>
  );
};

export default connect(Root);
```