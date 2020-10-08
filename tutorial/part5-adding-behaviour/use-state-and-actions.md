# Use 'state' and 'actions'

> *__[TO DO]__ modify this text to suit new context.*

Now let's learn how we can use `state` and `actions` within our theme to develop a bit of interactivity. We're going to add the option to show/hide the menu.

Open `index.js` at the root of our theme and add a new field called `isMenuOpen` in `state.theme`. We'll set it to default to `false`.

```jsx
// File: /packages/my-first-theme/src/index.js

import Root from "./theme-files";

const jsNation = {
  name: "my-first-theme",
  roots: {
    theme: Root
  },
  state: {
    theme: {
      isMenuOpen: false
    }
  },
  actions: {
    theme: {}
  }
};

export default jsNation
```

Then add two actions to change the value of this field. One of them will set the value to `true`, the other will set it to `false`. We'll use the state of this variable to determine whether the menu should be open or closed.

> This is the proper way to mutate state. You should never mutate the state directly from your components. You should, instead, create actions to mutate state and call those actions from your components.

```jsx
// File: /packages/my-first-theme/src/index.js

import Root from "./theme-files";

const jsNation = {
  name: "my-first-theme",
  roots: {
    theme: Root
  },
  state: {
    theme: {
      isMenuOpen: false
    }
  },
  actions: {
    theme: {
      openMenu: ({state}) => {
        state.theme.isMenuOpen = true
      },
      closeMenu: ({state}) => {
        state.theme.isMenuOpen = false
      }
    }
  }
};

export default jsNation
```

Now in the root component we'll add some conditional logic to check the value of `isMenuOpen` and either display the menu or not. Again we have to use the ternary conditional operator here.

```jsx
// File: /packages/my-first-theme/src/theme-files/index.js

// ...
{ state.theme.isMenuOpen ? (
    <Menu>
      <Link href="/">Home</Link>
      <Link href="/page/2">More posts</Link>
      <Link href="/lorem-ipsum">Lorem Ipsum</Link>
    </Menu>
  ) : null
}
```

You will find that the menu has disappeared, but if you change the value of `isMenuOpen` in `index.js` to `true` it will reappear. So let's add some buttons that use the actions we added earlier to change the value from the front end.

```jsx
// File: /packages/my-first-theme/src/theme-files/index.js

// ...

const Root = ({ state, actions }) => {

// ...

{state.theme.isMenuOpen ? (
  <>
    <button onClick={actions.theme.closeMenu}>Close</button>
    <Menu>
      <Link href="/">Home</Link>
      <Link href="/page/2">More posts</Link>
      <Link href="/lorem-ipsum">Lorem Ipsum</Link>
    </Menu>
  </>
  ) : (
      <button onClick={actions.theme.openMenu}>Menu</button>
  )
}
```

Note that we have to wrap the `button` element and `<Menu>` component in enclosing empty tags `<> ... </>`. Remember too that we need to pass `actions` to the `Root` component.

Finally let's create a styled `Button` component and use it in order to improve the appearance.

```jsx
// File: /packages/my-first-theme/src/theme-files/index.js

// ...
{state.theme.isMenuOpen ? (
  <>
    <Button onClick={actions.theme.closeMenu}>Close</Button>
    <Menu>
      <Link href="/">Home</Link>
      <Link href="/page/2">More posts</Link>
      <Link href="/lorem-ipsum">Lorem Ipsum</Link>
    </Menu>
  </>
  ) : (
      <Button onClick={actions.theme.openMenu}>Menu</Button>
  )
}
// ...
const Button = styled.button`
  width: 92px;
  margin: 1em 0 0;
  padding: 0.5em;
  background: white;
  border: 1px solid #aaa;
  color: #888;
`
```