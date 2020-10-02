# Style the components

> *__[TO DO]__ modify this text to suit new context.*

> *__[TO DO]__ this section is long - consider splitting it into 2 or more sections.*

Awesome, we now have a fully functioning website! But you're probably looking at it and thinking "I've seen prettier warthogs!" 🐗

Let's fix that.

Frontity uses CSS-in-JS for styling components. This has a number of advantages:

- it only loads the CSS needed for each page which improves the performance
- you don't have to worry about classes and problems with duplication, typos, etc
- you don't have to worry about vendor prefixing so you can write your CSS based on the current standard and Frontity handles the rest for you
- you can use all the power of JavaScript to style your components and create dynamic styles with much less code

> You can learn more about styling your Frontity app [here](https://docs.frontity.org/learning-frontity/styles).

> Frontity uses Emotion for CSS-in-JS. Find out more [here](https://emotion.sh/docs/introduction).

The first thing we will do is create global styles. These apply site-wide and should be added to the root component of your theme. We'll change the font to be sans-serif. To do this import the `<Global>` component and the `css` function from Frontity into our root component.

```jsx
// File: /packages/jsnation-theme/src/theme-files/index.js

// ...
import { connect, Global, css } from "frontity";

const Root = ({ state }) => {

  const data = state.source.get(state.router.link);

  return (
    <>
      <Global
        styles={css`
          html {
            font-family: sans-serif;
          }
        `}
      />
      {/* ... */}
    </>
  );
};
```

The `css` function takes as it's argument a template literal, which in this case consists of standard CSS contained within backticks. These styles are applied to the `styles` attribute on the `Global` component. When you save the file you should notice that the fonts on your site have changed automatically.

Now let's create some CSS components. These components are created using `styled`, which like `css` is a function. However the HTML tag that you want to style is appended with dot notation and then, again like `css`, the function takes a template literal containing CSS as it's argument.

As a basic example let's start by creating a `<Header>` component and give it a background colour, though first we need to import `styled` from Frontity.

```jsx
// File: /packages/jsnation-theme/src/theme-files/index.js

// ...
import { connect, Global, css, styled } from "frontity";
// ...

const Header = styled.header`
  background-color: #eee;
`
```

Once the `<Header>` component has been created let's use it in our root component to wrap all the elements that we want contained in the header section of our site.

```jsx
// File: /packages/jsnation-theme/src/theme-files/index.js

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
// File: /packages/jsnation-theme/src/theme-files/index.js

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
// File: /packages/jsnation-theme/src/theme-files/index.js

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
// File: /packages/jsnation-theme/src/theme-files/index.js

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
// File: /packages/jsnation-theme/src/theme-files/index.js

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
// File: /packages/jsnation-theme/src/theme-files/index.js

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
// File: /packages/jsnation-theme/src/theme-files/index.js

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
// File: /packages/jsnation-theme/src/theme-files/list.js

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
// File: /packages/jsnation-theme/src/theme-files/link.js

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
// File: /packages/jsnation-theme/src/theme-files/post.js

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