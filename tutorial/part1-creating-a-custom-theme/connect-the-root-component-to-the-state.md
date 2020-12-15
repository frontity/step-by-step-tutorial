# Connect the `<Root>` component to the state

Let’s now connect the `<Root>` component to the Frontity state using `connect`.

`connect` is a higher order component that takes a React component as an argument. It passes the Frontity state to the React component specified in the argument via props, and so enables a component in our theme to access data stored in the state.

{% hint style="info" %}
We'll be covering the Frontity state in detail shortly in the section entitled [Understanding the Frontity state](../part3-displaying-posts/understanding-the-frontity-state.md).
{% endhint %}

We need to `import { connect } from "frontity"`, pass `state` as a prop to our component, and finally export the connected component with `export default connect(Root)`.

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
  <img alt="Frontity in the browser" src="../assets/part1img5.png">
</p>

You can try changing the URL in the browser's address bar to something like http://localhost:3000/hello-frontity to see how the value of `state.router.link` changes.

<p>
  <img alt="Frontity in the browser" src="../assets/part1img6.png">
</p>
