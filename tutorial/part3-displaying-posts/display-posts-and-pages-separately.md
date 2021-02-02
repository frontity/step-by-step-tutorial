# Display posts and pages separately

We're making great progress and our theme now has a good deal of useful functionality! 🙌

At the moment posts and pages both use the same component. However, normally posts and pages would be displayed differently from one another. Posts, for example, would display author and date information as well as tags, categories, etc..., whereas pages would not.

Let's distinguish between the two now.

Create a new file and call it `page.js`. Copy the contents of `post.js` into `page.js` and rename the component from `<Post>` to `<Page>`. Remember to also change the `export` line - line 18 in the code sample below.

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
      <div dangerouslySetInnerHTML={{ __html: page.content.rendered }} />
    </div>
  )
}

export default connect(Page)
```

{% hint style="info" %}
Here we can see why it was a good idea to use `data.type` rather than hard code `post`, because in this case the type will be `page`.
{% endhint %}

At the moment `page.js` and `post.js` are pretty much identical, so let's now distinguish between them by adding author and date info to `post.js`.

If we take a look at the data about a post, so for example `frontity.state.source.post[60]`, we can see that the only information we have about the author is the ID.

<p>
  <img alt="Frontity in the console" src="../assets/part3img11.png">
</p>

We can use this ID to get the actual author information from `state.source.author[ID]`.

<p>
  <img alt="Frontity in the console" src="../assets/part3img12.png">
</p>

Let's modify the `<Post>` component in `post.js` to get the author information and display both it and the post date.

```jsx
// File: /packages/my-first-theme/src/components/post.js

import React from "react"
import { connect } from "frontity"

const Post = ({ state }) => {
  const data = state.source.get(state.router.link)
  const post = state.source[data.type][data.id]
  const author = state.source.author[post.author]

  return (
    <div>
      <h2>{post.title.rendered}</h2>
      <p>
        <strong>Posted: </strong>
        {post.date}
      </p>
      <p>
        <strong>Author: </strong>
        {author.name}
      </p>
      <div dangerouslySetInnerHTML={{ __html: post.content.rendered }} />
    </div>
  )
}

export default connect(Post)
```

Finally in this section let's change the root component file to import the `<Page>` component, and then use it in the `<Switch>` component to conditionally render it if `data.isPage` is true.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
import Page from "./page"

const Root = ({ state }) => {
  const data = state.source.get(state.router.link)

  return (
    <>
      {/* ... */}
      <Switch>
        <List when={data.isArchive} />
        <Post when={data.isPost} />
        <Page when={data.isPage} />
      </Switch>
    </>
  )
}
```

Now as you navigate around the site and view posts and pages a different component is used for each case and you'll notice that posts, e.g. _"The Beauties of Gullfoss"_, have the author and date info, but pages, e.g. _"About Us"_, do not.

<p>
  <img alt="Frontity in the browser" src="../assets/part3img13.png" width="565" height="161">
</p>

{% hint style="success" %}
**Check you're on the right track** by comparing your changes with [the ones in this commit](https://github.com/frontity-demos/tutorial-hello-frontity/commit/cfcb5aa1e18d30cf4d2250bb262569a571ee7217).
{% endhint %}
