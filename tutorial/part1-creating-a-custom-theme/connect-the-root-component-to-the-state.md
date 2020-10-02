# Connect the `<Root>` component to the state

> ***[TO DO]** modify this text to suit new context.*

> ***[TO DO]** explain `connect` and how it's used to pass the Frontity state to the React components via props.*

Let’s connect the `<Root>` component to the Frontity state using `connect`. This allows us to access data stored in the state.

We need to `import {connect} from "frontity"`, pass `state` as a prop to our component, and finally export the connected component.

Then we add a `<p>` element to our component to display the URL we are currently in using `state.router.link`.

```jsx
// File: /packages/jsnation-theme/src/theme-files/index.js

import React from "react";
import { connect } from "frontity";

const Root = ({ state }) => {
  return (
    <>
      <h1>Frontity Workshop</h1>
      <p>Current URL: {state.router.link}</p>
    </>
  );
};

export default connect(Root);
```
You can try changing the URL in the browser's address bar to something like http://localhost:3000/hello-frontity to see how the `state.router.link` changes.