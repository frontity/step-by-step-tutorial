# Use the `<html2react>` component

At the moment we have a problem with internal links in our content. For example, look at the post entitled "Latest Trip to India". The link to "New7Wonders of the World" at the bottom of the post forces SSR and a page reload. Another example can be found in the post entitled "Shinjuku Gyoen National Garden". The link "post about the Banff National Park" also forces SSR and a page reload. More examples can be found on the "About Us" page.

Frontity provides a number of components, one of which is `<html2react>`. This enables us to process our content and replace HTML elements with React components. We can use `<html2react>` to replace any `<a href="...">` links in our content with the `<Link>` component. You'll remember that we've previously used the `<Link>` component directly in our menu and in our list page.

Check the file `frontity.settings.js`. You should find that `"@frontity/html2react"` is already included in the `packages` array of our project.

First we need to import the link processor into our `<Root>` component, and also add it to the array of `html2react` processors on the `libraries` object.

Add this to the root level `index.js` file.

```jsx
// File: /packages/my-first-theme/src/index.js

import link from "@frontity/html2react/processors/link";

// ...
roots: {...},
state: {...},
actions: {...},
libraries: {
  html2react: {
    processors: [link]
  }
}
```

Now, inside our `<Post>` component in `post.js` let's pass `libraries` in as a prop and get the component ready for use.

```jsx
// File: /packages/my-first-theme/src/components/post.js

// ...
const Post = ({ state, libraries }) => {

  // ...
  const Html2React = libraries.html2react.Component;
  // ...

}
```

Finally, replace this:

```jsx
  <div dangerouslySetInnerHTML={{ __html: post.content.rendered }} />
```

with this:

```jsx
  <Html2React html={post.content.rendered} />
```

And now the internal links in our posts will update from the state and not force an HTTP request and hence a page reload.

You should also do the same for the `<Page>` component in `page.js`, which should ultimately look like this:

```jsx
import React from "react";
import { connect } from "frontity";

const Page = ({ state, libraries }) => {

  const data = state.source.get(state.router.link);
  const post = state.source[data.type][data.id];

  const Html2React = libraries.html2react.Component;

  return (
    <div>
      <h2>{post.title.rendered}</h2>
      <Html2React html={post.content.rendered} />
    </div>
  );

};

export default connect(Page);
```

And now the links on the `About Us` page should work as expected as well.

See [our docs here](https://docs.frontity.org/api-reference-1/frontity-html2react) for more on the `@frontity/html2react` package.