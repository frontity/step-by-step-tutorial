# Display the list of posts

> *__[TO DO]__ modify this text to suit new context.*

> *__[TO DO]__ explain the “two-step” access to data.*

In order to display the list of posts, let's create a new file in the `components` folder and call it `list.js`.

This will contain a component called `<List>` which will show the information in `state.source.data`, namely the `type`, `id` and `link` of each post.

```jsx
// File: /packages/my-first-theme/src/components/list.js

import React from "react";
import { connect } from "frontity";

const List = ({ state }) => {

  const data = state.source.get(state.router.link);

  return (
    <div>
      {data.items.map(item => {
        return (
          <div key={item.id}>
            {item.type} – {item.id} – {item.link}
          </div>
        );
      })}
    </div>
  );

};

export default connect(List);
```

We need to import it into our root component and use it.

```jsx
// File:  /packages/my-first-theme/src/components/index.js

// ...
import List from "./list";

const Root = ({ state }) => {

  const data = state.source.get(state.router.link);

  return (
    <>
      {/* ... */}
      <main>
        <Switch>
          <List when={data.isArchive} />
          <div when={data.isPost}>This is a post</div>
          <div when={data.isPage}>This is a page</div>
        </Switch>
      </main>
    </>
  );

};
```

Great! Now we can see some information about each of the posts on the `Home` page and on the `More posts` page.

<p>
  <img alt="Frontity in the browser" src="../assets/part3img6.png">
</p>

Now let's change the `<List>` component to use the information about each of the posts to show the title and turn it into a link. Remember to import the `<Link>` component into `list.js`!

```jsx
// File: /packages/my-first-theme/src/components/list.js

import React from "react";
import { connect } from "frontity";
import Link from "@frontity/components/link";

const List = ({ state }) => {

  const data = state.source.get(state.router.link);

  return (
    <div>
      {data.items.map(item => {
        const post = state.source[item.type][item.id]
        return (
          <Link key={item.id} link={post.link}>
            {post.title.rendered}<br/>
          </Link>
        );
      })}
    </div>
  );

};
```

Now our list page is a series of links to individual posts.

<p>
  <img alt="Frontity in the browser" src="../assets/part3img7.png">
</p>

And if we click a link we can see finally see the text "This is a post".

<p>
  <img alt="Frontity in the browser" src="../assets/part3img8.png">
</p>

However, what we really want to see is the post content. Let's do that next.