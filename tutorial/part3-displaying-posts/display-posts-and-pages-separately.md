# Display posts and pages separately

> *__[TO DO]__ modify this text to suit new context.*

> *__[TO DO]__ Make use of `isPost` of `isPage`  (Frontity Magic in action!).*

> *__[TO DO]__ Different component for different content type (Custom component creation).*

> *__[TO DO]__ Maybe use one component but with conditionals to display post and page differently.*

At the moment posts and pages both use the same component. But normally posts will display author and date information as well as tags, categories, etc...

Let's distinguish between the two now.

Create a new file and call it `page.js`. Copy the contents of `post.js` into `page.js` and rename the component.

```jsx
// File: /packages/my-first-theme/src/components/page.js

import React from "react"
import { connect } from "frontity"

const Page = ({ state }) => {
    const data = state.source.get(state.router.link)
    const page = state.source[data.type][data.id]

    return (
        <div>
            <h2>{page.title.rendered}</h2>
            <div dangerouslySetInnerHTML={{ __html: page.content.rendered}} />
        </div>
    )
}

export default connect(Page)
```

At the moment `page.js` and `post.js` are pretty much identical, so let's now distinguish between them by adding author and date info to `post.js`.

```jsx
// File: /packages/my-first-theme/src/components/post.js

import React from "react";
import { connect } from "frontity";

const Post = ({ state }) => {
  const data = state.source.get(state.router.link);
  const post = state.source[data.type][data.id];
  const author = state.source.author[post.author]

  return (
    <div>
      <h2>{post.title.rendered}</h2>
      <p><strong>Posted: </strong>{post.date}</p>
      <p><strong>Author: </strong>{author.name}</p>
      <div dangerouslySetInnerHTML={{ __html: post.content.rendered }} />
    </div>
  );
};

export default connect(Post);
```

Finally in this section let's change the root component to import and use the `<Page>` component.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
import Page from "./page"

const Root = ({ state }) => {
  const data = state.source.get(state.router.link);

  return (
    <>
      {/* ... */}
      <main>
        {data.isArchive && <List />}
        {data.isPost && <Post />}
        {data.isPage && <Page />}
      </main>
    </>
  );
};
```

Now as you navigate around the site and view posts and pages you 'll notice that posts have the author and date info but pages do not.