# Add pagination

A key feature of any traditional, i.e. PHP-based, WordPress theme is the ability to paginate through the post listing. In this lesson we will look at implementing this feature in Frontity.

Click on the `More posts` link in the menu to navigate to `/page/2` and examine `frontity.state` in the console. You will notice that the data for the page has both `previous` and `next` properties.

<p>
  <img alt="Frontity in the console" src="../assets/part5img1.png" width="700">
</p>

> _If you do the same for the home path, i.e. '/', you will notice that it doesn't have a `previous` property._

We can use these properties to add pagination to our `<List>` component. We will add a `<PrevNextNav>` component to style two buttons that enable us to page through the lists of posts.

Change `list.js` as follows. Note that we need to pass `actions` into the `<List>` component.

```jsx
// File: /packages/my-first-theme/src/components/list.js

import React from "react"
import { connect, styled } from "frontity"
import Link from "@frontity/components/link"

const List = ({ state, actions }) => {
  const data = state.source.get(state.router.link)

  return (
    <Items>
      {data.items.map((item) => {
        const post = state.source[item.type][item.id]
        return (
          <Link key={item.id} link={post.link}>
            {post.title.rendered}
          </Link>
        )
      })}
      <PrevNextNav>
        {data.previous && (
          <button
            onClick={() => {
              actions.router.set(data.previous)
            }}
          >
            &#171; Prev
          </button>
        )}
        {data.next && (
          <button
            onClick={() => {
              actions.router.set(data.next)
            }}
          >
            Next &#187;
          </button>
        )}
      </PrevNextNav>
    </Items>
  )
}

export default connect(List)

const Items = styled.div`
  & > a {
    display: block;
    margin: 6px 0;
    font-size: 1.2em;
    color: steelblue;
    text-decoration: none;
  }
`
const PrevNextNav = styled.div`
  padding-top: 1.5em;

  & > button {
    background: #eee;
    text-decoration: none;
    padding: 0.5em 1em;
    color: #888;
    border: 1px solid #aaa;
    font-size: 0.8em;
    margin-right: 2em;
  }
  & > button:hover {
    cursor: pointer;
  }
`
```

We've included conditional checks so that the 'Previous' button doesn't show on the first page and the 'Next' button doesn't show on the last page, as they're not needed in those locations. To do this we've used ["short-circuit" evaluation](https://en.wikipedia.org/wiki/Short-circuit_evaluation).

---

Now that we have pagination we no longer need the 'More posts' option in the menu. Let's remove it.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
const Root = ({ state, actions }) => {

  // ...
  <Header isPostType={data.isPostType} isPage={data.isPage}>
    <HeaderContent>
      // ...
      <Menu>
        <Link link="/">Home</Link>
        <Link link="/about-us">About Us</Link>
      </Menu>
    </HeaderContent>
  </Header>
  <Main>
    // ...
  </Main>
    // ...
};
```
