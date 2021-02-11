# Styling the links

In this lesson we're going to style all the links in our site. We have links in the header menu and on the post listing pages.

First let's turn our attention to the header section and style the menu. We'll make our links a consistent colour and remove the underlines so that it looks a bit cleaner. To do this we'll add a `Menu` component which will be a styled `<nav>` element.

It's useful to know that the `<Link>` component returns an `<a>` element. Knowing this we can apply styles to any `<a>` elements inside our styled `<nav>` element.

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
      <Link link="/">Home</Link>
      <Link link="/page/2">More posts</Link>
      <Link link="/about-us">About Us</Link>
    </Menu>
  </HeaderContent>
</Header>
// ...
```

We now have a more pleasing looking header.

Next we'll improve the appearance of our `<List>` component by having the links in our list rendered in the same style as the menu.

So far we've added all our styled components to the `index.js` file for use in the `<Root>` component. Now we'll open `list.js` and add an `<Items>` component which will be a styled `<div>` element. We'll then use it within the `<List>` component as a wrapper around all the post title links.

{% hint style="info" %}
☝️ Remember also to import `styled` from `frontity` into `list.js`.
{% endhint %}

```jsx
// File: /packages/my-first-theme/src/components/list.js

import React from "react"
import { connect, styled } from "frontity"
import Link from "@frontity/components/link"

const List = ({ state }) => {
  const data = state.source.get(state.router.link)

  return (
    <Items>
      {data.items.map((item) => {
        const post = state.source.post[item.id]
        return (
          <Link link={post.link} key={post.id}>
            {post.title.rendered}
          </Link>
        )
      })}
    </Items>
  )
}

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

Great, things are starting to look pretty good! 🎉

{% hint style="success" %}
**Check you're on the right track** by comparing your changes with [the ones in this commit](https://github.com/frontity-demos/tutorial-hello-frontity/commit/0f8ed3e17c0daaf151935bdf72ad04cbc6be9bd6).
{% endhint %}
