# Style the components

> *__[TO DO]__ modify this text to suit new context.*

> *__[TO DO]__ this section is long - consider splitting it into 2 or more sections.*

Now let's create some CSS components. These components are created using `styled`, which like `css` is a function. However the HTML tag that you want to style is appended with dot notation and then, again like `css`, the function takes a template literal containing CSS as it's argument.

As a basic example let's start by creating a `<Header>` component and give it a background colour, though first we need to import `styled` from Frontity.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
import { connect, Global, css, styled } from "frontity";
// ...

const Header = styled.header`
  background-color: #eee;
`
```

Once the `<Header>` component has been created let's use it in our root component to wrap all the elements that we want contained in the header section of our site.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
const Root = ({ state, actions }) => {

  const data = state.source.get(state.router.link)

  return (
    <>
      <Global
        styles={css`
        html {
            font-family: sans-serif;
        }
      `}
      />
      <Header>
        <h1>Frontity Workshop</h1>
        <p>Current URL: {state.router.link}</p>
        <nav>
          <Link href="/">Home</Link>
          <Link href="/page/2">More posts</Link>
          <Link href="/lorem-ipsum">Lorem Ipsum</Link>
        </nav>
      </Header>
      <main>
        {data.isArchive && <List />}
        {data.isPost && <Post />}
        {data.isPage && <Page />}
      </main>
    </>
  );
};
```

Now our header is contained within a nice light grey background. But notice the rather ugly white border around it. Let's fix that by applying a basic CSS reset to our `<Global>` component.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
<Global
        styles={css`
        * {
            padding: 0;
            margin: 0;
            box-sizing: border-box;
        }
        html {
            font-family: sans-serif;
        }
      `}
      />
// ...
```

This simple CSS reset will make styling our elements going forward much simpler with more consistent behaviour.

Let's continue styling our header by adding a border to the bottom.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...

const Header = styled.header`
  background-color: #eee;
  border-width: 0 0 8px 0;
  border-style: solid;
  border-color: maroon;
`
```

We also want to constrain our page width to 800px. To do that we will need to add a couple of extra components, `<HeaderContent>` and `<Main>`. Let's add these, and we'll also style some elements within Main.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
const Header = styled.header`
  background-color: #eee;
  border-width: 0 0 8px 0;
  border-style: solid;
  border-color: maroon;
`
const HeaderContent = styled.div`
    max-width: 800px;
    padding: 2em 1em;
    margin: auto;
`
const Main = styled.main`
    max-width: 800px;
    padding: 1em;
    margin: auto;

    img {
        max-width: 100%;
    }
    h2 {
        margin: 0.5em 0;
    }
    p {
        line-height: 1.25em;
        margin-bottom: 0.75em;
    }
`
```

And again we'll use those elements in our root component.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
const Root = ({ state, actions }) => {

  const data = state.source.get(state.router.link)

  return (
    <>
      <Global
        styles={css`
        html {
            font-family: sans-serif;
        }
      `}
      />
      <Header>
        <HeaderContent>
          <h1>Frontity Workshop</h1>
          <p>Current URL: {state.router.link}</p>
          <nav>
            <Link href="/">Home</Link>
            <Link href="/page/2">More posts</Link>
            <Link href="/lorem-ipsum">Lorem Ipsum</Link>
          </nav>
        </HeaderContent>
      </Header>
      <Main>
        {data.isArchive && <List />}
        {data.isPost && <Post />}
        {data.isPage && <Page />}
      </Main>
    </>
  );
};
```

Incidentally, this is where the [WordPress Theme Unit Test](https://github.com/WPTT/theme-unit-test) really starts to come into it's own. Since all post and page content is going to appear within the `<Main>` component you can keep adding elements to the definition of that component and styling them until all the unit tests pass. This will ensure that your theme is robust and will properly render any content that gets thrown at it. So far we've only minimally styled `img`, `h2`, and `p`.

For now though we'll turn our attention back to the header section and style the menu...

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
const Menu = styled.nav`
    display: flex;
    flex-direction: row;
    margin-top: 1em;
    & > div {
        margin-right: 1em;
    }
`
```

...and replace the `nav` element in our `Root` component with the new `Menu` component.

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
      <Link href="/lorem-ipsum">Lorem Ipsum</Link>
    </Menu>
  </HeaderContent>
</Header>
// ...
```

We now have a pleasing looking header.

Let's improve the appearance of our `<List>` component. Open `list.js` and add an `<Items>` component and use it with `<List>`. Remember also to import `styled` from `frontity`.

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
  & > div {
      margin: 12px 0;
      font-size: 1.2em;
  }
`
```

Now let's make all our links a consistent colour.

```jsx
// File: /packages/my-first-theme/src/components/link.js

import React from "react"
import { connect, styled } from "frontity"

const Link = ({href, actions, children}) => {
  return (
    <div>
      <Anchor
        href={href}
        onClick={e => {
          e.preventDefault()
          actions.router.set(href)
        }}
      >
        {children}
      </Anchor>
    </div>
  )
}

export default connect(Link)

const Anchor = styled.a`
    color: steelblue;
    text-decoration: none;
`
```

And finally for this section we'll highlight the author and date info in our `<Post>` component. Import `styled` into `post.js` and create and use a `<PostInfo>` component.

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