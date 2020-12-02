# Add tags to the `<head>` element

We're getting pretty close to having a finished site now, one that is fully-featured and looks good. But how is anyone going to find it?

One thing we've yet to take into account is SEO. To boost the chances of our site appearing in the search engine listings we'll add some tags to the `<head>` of our document. Tags such as `title` and `description` can be important for SEO so it's good practice if our theme includes them.

Let's import the `<Head>` component into our root component file. Then anything that we include within `<Head>...</Head>` tags will be included in the `<head>` section of the HTML document sent to the browser.

```jsx
// File: /packages/my-first-theme/src/components/index.js

import { ..., Head } from "frontity";

// ...

const Root = ({ state, actions }) => {
  const data = state.source.get(state.router.link);

  return (
    <>
      <Head>
        <title>My First Frontity Theme</title>
        <meta
          name="description"
          content="Based on the Frontity step by step tutorial"
        />
      </Head>
      ...
    </>
  );
};
```

As it’s a React component, you can include it wherever you like. There’s no need for it to be in the `<Root>` component. Additionally you can use variables so that the tags change dynamically, just as you can with any other React component.

You should already see the title appearing in the tab of you browser, and if you check your document with the browser devtools you should see the title and the description showing up.

<p>
  <img alt="Frontity in the console" src="../assets/part7img3.png" width="800">
</p>
