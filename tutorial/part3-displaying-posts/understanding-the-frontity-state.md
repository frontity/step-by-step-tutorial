# Understanding the Frontity state

> *__[TO DO]__ modify this text to suit new context.*

> *__[TO DO]__ new images may be required.*

In order to gain a better understanding of Frontity, let’s dig a little deeper and investigate how it works below the surface.

To do so, access `http://localhost:3000/about-us/` in the browser. The simplest way is to  click the link in the menu we've just created. We recommend that you then refresh the page to clear out the state.

When you've done that open the browser console. In the console type `frontity.state` to see the Frontity state. This is the same state that the components and actions have access to.

<p>
  <img alt="Frontity in the console" src="../assets/part3img1.png">
</p>

> Frontity uses [ES2015 Proxies](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy), so you have to open the property `[[Target]]` in order to see the state.

You will see Frontity's global state, including the general properties of your Frontity project. You can also see information about the `router`, including the `state.router.link` that we used earlier, and `source`, the package that connects Frontity to your WordPress site.

Let’s take a look at `state.source.data`. This is where the information for each URL is stored. If you inspect `/about-us/`, you can see that it’s a page, and that it has the ID 184.

<p>
  <img alt="Frontity in the console" src="../assets/part3img2.png" width="600">
</p>

With that information, we can access the data (title, content, etc) of that page with `state.source.page[184]`:

<p>
  <img alt="Frontity in the console" src="../assets/part3img3.png">
</p>

As you navigate from one URL to another, the package `@frontity/wp-source` automatically fetches everything you need and stores it in `state.source`.

If we open the Network tab (in the browser's devtools) and click on the menu to go to Home (Homepage), you will see that a call to the REST API is made to get the latest posts.

<p>
  <img alt="Browser developer tools network tab showing fetch" src="../assets/part3img4.png" width="700">
</p>


Take another look at `state.source.data`. You will notice that it's been populated with much more data than before.

Please note that instead of using `state.source.data[url]` it’s better to use the `get` helper function: `state.source.get(url)`. This ensures that URLs always include the final slash (/).

So now let’s inspect the homepage using state.source.get("/"):

<p>
  <img alt="Frontity in the console" src="../assets/part3img5.png">
</p>

As you can see, it has several interesting properties such as `isHome`, `isArchive`, and an array of `items`. If the homepage were a category it would have an `isCategory` property. If it were a post it would have an `isPost` property, etc... These are boolean values so we just need to check for their truthiness.

To wrap up this section let's use all of this in our code.

In this next step we **`get`** the information about the current link (`state.router.link`) and use it inside a `<main>` element to see whether it’s a `list`, a `post`, or a `page`.

To do this we'll use the `<Switch>` component. This acts like the 'switch' statement in any programming language, the first matching condition is the one that is executed. But first we need to import the `<Switch>` component. You can learn more about the `<Switch>` component [in our docs](https://docs.frontity.org/api-reference-1/frontity-components#switch).

```jsx
// File: /packages/my-first-theme/src/components/index.js
import Switch from "@frontity/components/switch";

const Root = ({ state }) => {

  const data = state.source.get(state.router.link);

  return (
    <>
      <h1>Hello Frontity</h1>
      <p>Current URL: {state.router.link}</p>
      <nav>
        <Link link="/">Home</Link><br />
        <Link link="/page/2">More posts</Link><br />
        <Link link="/about-us">About Us</Link>
      </nav>
      <hr />
      <main>
        <Switch>
          <div when={data.isArchive}>This is a list</div>
          <div when={data.isPost}>This is a post</div>
          <div when={data.isPage}>This is a page</div>
        </Switch>
      </main>
    </>
  );
};
```

Since we don't yet have any links to any posts the second condition will never be satisfied, so we won't ever see the text "This is a post" come up. Let's go on to address that.