# Styling the post info

In this lesson we'll highlight the author and date info in our `<Post>` component so that they stand out from the rest of the post content.

Import `styled` into `post.js` and create and use a `<PostInfo>` component.

```jsx
// File: /packages/my-first-theme/src/components/post.js

import React from "react"
import { connect, styled } from "frontity"

const Post = ({ state }) => {
  const data = state.source.get(state.router.link)
  const post = state.source[data.type][data.id]
  const author = state.source.author[post.author]

  return (
    <div>
      <h2>{post.title.rendered}</h2>
      <PostInfo>
        <p>
          <strong>Posted: </strong>
          {post.date}
        </p>
        <p>
          <strong>Author: </strong>
          {author.name}
        </p>
      </PostInfo>
      <div dangerouslySetInnerHTML={{ __html: post.content.rendered }} />
    </div>
  )
}

export default connect(Post)

const PostInfo = styled.div`
  background-image: linear-gradient(to right, #f4f4f4, #fff);
  margin-bottom: 1em;
  padding: 0.5em;
  border-left: 4px solid lightseagreen;
  font-size: 0.8em;

  & > p {
    margin: 0;
  }
`
```

Visit one of the posts now and the date and author info are pleasingly highlighted.

For reference, this is what your site should be looking like now:

<p>
  <img alt="Frontity in the browser - listing" src="../assets/part4img1.png">
</p>

<p>
  <img alt="Frontity in the browser - post" src="../assets/part4img2.png">
</p>
