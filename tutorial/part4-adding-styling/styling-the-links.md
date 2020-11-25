# Styling the links

First let's turn our attention to the header section and style the menu. We'll make our links a consistent colour and remove the underlines so that it looks a bit cleaner by adding a `Menu` component.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
const Menu = styled.nav`
    display: flex;
    flex-direction: row;
    margin-top: 1em;
    & > a {
        margin-right: 1em;
        color: steelblue;
        text-decoration: none;
    }
`
```

Now we can replace the `nav` element in our `Root` component with the new `Menu` component.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
 <Header>
  <HeaderContent>
    <h1>Frontity Workshop</h1>
    <p>Current URL: {state.router.link}</p>
    <Menu>
      <Link href="/">Home</Link>
      <Link href="/page/2">More posts</Link>
      <Link link="/about-us">About Us</Link>
    </Menu>
  </HeaderContent>
</Header>
// ...
```

We now have a more pleasing looking header.

Let's improve the appearance of our `<List>` component by having our links in the same style as the menu.

So far we've added all our styled components to the `index.js` file for use in the `Root` component. Now we'll open `list.js` and add an `<Items>` component and use it with `<List>`. Remember also to import `styled` from `frontity`.

```jsx
// File: /packages/my-first-theme/src/components/list.js

import React from "react"
import { connect, styled } from "frontity"
import Link from "./link"

const List = ({ state }) => {
  const data = state.source.get(state.router.link);

  return (
    <Items>
      {data.items.map(item => {
        const post = state.source.post[item.id];
        return (
          <Link href={post.link} key={post.id}>
            {post.title.rendered}
          </Link>
        );
      })}
    </Items>
  );
};

const Items = styled.div`
  & > a {
    display: block;
    margin: 6px 0;
    font-size: 1.2em;
    color: steelblue;
    text-decoration: none;
  }
`
```

Finally for this section we'll highlight the author and date info in our `<Post>` component. Import `styled` into `post.js` and create and use a `<PostInfo>` component.

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
                <p><strong>Posted: </strong>{post.date}</p>
                <p><strong>Author: </strong>{author.name}</p>
            </PostInfo>
            <div dangerouslySetInnerHTML={{ __html: post.content.rendered}} />
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