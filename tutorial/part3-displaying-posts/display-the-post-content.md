# Display the post content

At the moment we have a list of clickable post links, but when we click them we simply see the text "This is a post". However you will notice that the URL is changing. This then is a good place to display the content of each post.

Let's create a new file called `post.js` inside the `components` folder. This will contain the `<Post>` component which we will use to display the title and the content of the posts.

Note the use of the two step data retrieval process in this code. We first use `state.source.get`, the helper function, to get the relevant item from `state.source.data`, and then we use the `data.type` property to determine where in the state we should fetch the item from, i.e. whether it's a post or a page.

```jsx
// File: /packages/my-first-theme/src/components/post.js

import React from "react"
import { connect } from "frontity"

const Post = ({ state }) => {
  const data = state.source.get(state.router.link)
  const post = state.source[data.type][data.id]

  return (
    <div>
      <h2>{post.title.rendered}</h2>
      <div dangerouslySetInnerHTML={{ __html: post.content.rendered }} />
    </div>
  )
}

export default connect(Post)
```

As before, we need to import it into the root component file and use it to display posts and pages.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
import Post from "./post"

const Root = ({ state }) => {
  const data = state.source.get(state.router.link)

  return (
    <>
      {/* ... */}
      <Switch>
        <List when={data.isArchive} />
        <Post when={data.isPost} />
        <Post when={data.isPage} />
      </Switch>
    </>
  )
}
```

Note that for now we are using the `<Post>` component whether `data.isPost` or `data.isPage` is true.

Now we can see the post title and the content. 🙌
