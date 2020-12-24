# Use 'state' and 'actions'

Now let's learn how we can use `state` and `actions` within our theme to develop a bit of interactivity.

We're going to add the option to show/hide the URL that sits just under our main heading. We originally used this to display the value of `state.router.link` when we first connected our `<Root>` component to the state in an [earlier lesson](part1-creating-a-custom-theme/connect-the-root-component-to-the-state.md).

Open `index.js` at the root of our theme and add a new boolean property called `isUrlVisible` in `state.theme`. We'll set its default value to `false`.

```jsx
// File: /packages/my-first-theme/src/index.js

import Root from "./components"

const myFirstTheme = {
  name: "my-first-theme",
  roots: {
    theme: Root,
  },
  state: {
    theme: {
      isUrlVisible: false,
    },
  },
  actions: {
    theme: {},
  },
}

export default myFirstTheme
```

Now in the `<HeaderContent>` component within the `<Root>` component we'll add some conditional logic to check the value of `isUrlVisible` and either display the URL or not. Again we have to use the ternary conditional operator here.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
<Header isPostType={data.isPostType} isPage={data.isPage}>
  <HeaderContent>
    <h1>Hello Frontity</h1>
    { state.theme.isUrlVisible ? <p>Current URL: {state.router.link}</p> : null }
    <Menu>
      // ...
    </Menu>
  </HeaderContent>
</Header>
<Main>
  // ...
</Main>
```

When you save the file you will find that the URL has disappeared, but if you change the value of `isUrlVisible` in `index.js` to `true` it will reappear. Try it now! _(**note**: you may have to manually refresh the browser)_

```jsx
// File: /packages/my-first-theme/src/index.js

//...
  state: {
    theme: {
      isUrlVisible: true,
    },
  },
//...
```

As we've just seen, the state of the `isUrlVisible` variable determines whether the URL is visible or not.

Next we'll add an action - this is a function, which we'll call `toggleUrl`, that will toggle the value of `isUrlVisible` between true and false.

{% hint style="info" %}
**NOTE:** This is the proper way to mutate state. You should never mutate the state directly from your components. You should, instead, create actions to mutate state and call those actions from your components.
{% endhint %}

```jsx
// File: /packages/my-first-theme/src/index.js

import Root from "./components"

const myFirstTheme = {
  name: "my-first-theme",
  roots: {
    theme: Root,
  },
  state: {
    theme: {
      isUrlVisible: false,
    },
  },
  actions: {
    theme: {
      toggleUrl: ({ state }) => {
        state.theme.isUrlVisible = !state.theme.isUrlVisible
      },
    },
  },
}

export default myFirstTheme
```

Let's add some buttons that use the `toggleUrl` action we just added to change the value of `isUrlVisible` from the front end.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...

const Root = ({ state, actions }) => {

// ...
{ state.theme.isUrlVisible
  ? <>Current URL: {state.router.link} <button onClick={actions.theme.toggleUrl}>&#x3c; Hide URL</button></>
  : <button onClick={actions.theme.toggleUrl}>Show URL &#x3e;</button>
}
```

Note that we have to wrap the `button` element and "Current URL" string in enclosing empty tags `<> ... </>`.

{% hint style="info" %}
☝️ Remember too that we need to pass `actions` to the `<Root>` component in order to use the `toggleUrl` function that we defined earlier.
{% endhint %}

Great, now we can show or hide the URL with user actions in the browser.

Finally let's create a styled `<Button>` component and use it in place of the `<button>` element in order to improve the appearance.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
{
  state.theme.isUrlVisible ? (
    <>
      Current URL: {state.router.link}{" "}
      <Button onClick={actions.theme.toggleUrl}>&#x3c; Hide URL</Button>
    </>
  ) : (
    <Button onClick={actions.theme.toggleUrl}>Show URL &#x3e;</Button>
  )
}
// ...
const Button = styled.button`
  background: transparent;
  border: none;
  color: #aaa;

  :hover {
    cursor: pointer;
    color: #888;
  }
`
```
