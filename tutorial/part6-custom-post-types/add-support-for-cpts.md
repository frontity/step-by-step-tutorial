# Add support for custom post types

> *__[TO DO]__ new content to be written.*

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
    </>
  );
};
```

Add support for custom post types in`frontity.settings.js`

