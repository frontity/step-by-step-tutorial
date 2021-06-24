# Connect the `<Root>` component to the state

Let’s now connect the `<Root>` component to the Frontity state using `connect`.

`connect` is a higher order component that takes a React component as an argument. It passes the Frontity object to the React component specified in the argument via props. The Frontity object has amongst its properties `state`, `actions` and `libraries`. `connect` therefore enables a component in our theme to access data stored in the `state`, or functions available in `actions`.

This also ensures that the component is re-rendered whenever any value from the state which the component is using is changed.

{% hint style="info" %}
We'll be covering the Frontity state in detail shortly in the section entitled [Understanding the Frontity state](../part3-displaying-posts/understanding-the-frontity-state.md).
{% endhint %}

In order to connect our component to the Frontity state we need to `import { connect } from "frontity"`, pass `state` as a (destructured) prop to our component, and finally export the connected component with `export default connect(Root)`.

We can check that our `<Root>` component is connected to the state by adding a `<p>` element to our component to display the URL we are currently in. We can do this by using `state.router.link`.

```jsx
// File: /packages/my-first-theme/src/components/index.js

import React from "react"
import { connect } from "frontity"

const Root = ({ state }) => {
  return (
    <>
      <h1>Frontity Workshop</h1>
      <p>Current URL: {state.router.link}</p>
    </>
  )
}

export default connect(Root)
```

Now when you save the file we can see that we are in the root of our site: `/`.

<p>
  <img alt="Frontity in the browser" src="https://frontity.org/wp-content/uploads/2021/04/frontity-tutorial-part1img5.png">
</p>

You can try changing the URL in the browser's address bar to something like http://localhost:3000/about-us to see how the value of `state.router.link` changes.

<p>
  <img alt="Frontity in the browser" src="https://frontity.org/wp-content/uploads/2021/04/frontity-tutorial-part1img6.png">
</p>

{% hint style="success" %}
**Check you're on the right track** by comparing your changes with [the ones in this commit](https://github.com/frontity-demos/tutorial-hello-frontity/commit/eebb495ba16ede2d310bc838396aca662df5f3bc).
{% endhint %}
