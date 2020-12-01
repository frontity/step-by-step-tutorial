# Add tags to the `<head>` element

> *__[TO DO]__ modify this text to suit new context.*

> *__[TO DO]__ add more explanation here.*

> *__[TO DO]__ image needs updating.*

You can use React to add tags to the `<head>` of your document. Tags such as a title and a description can be important for SEO so it's good practice if your theme includes them.

Import the `<Head>` component, and everything you include within `<Head>...</Head>` tags will be included in the `<head>` section of your document.

```jsx
// File: /packages/my-first-theme/src/components/index.js

import { ..., Head } from "frontity";

// ...

const Root = ({ state, actions }) => {
  const data = state.source.get(state.router.link);

  return (
    <>
      <Head>
        <title>Frontity Workshop at JS Nation</title>
        <meta name="description" content="An introduction to creating a theme with Frontity" />
      </Head>
      {/* ... */}
  );
};
```

As it’s a React component, you can include it wherever you like. There’s no need for it to be in the `<Root>` component. Additionally you can use variables so that the tags change dynamically, just as you can with any other React component.

Check your document with the browser devtools and you should see these showing up.

<p>
  <img alt="Frontity in the console" src="../assets/part7img3.png" width="800">
</p>