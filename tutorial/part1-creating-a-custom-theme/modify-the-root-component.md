# Modify the `<Root>` component

Let's continue by seeing how we can get Frontity to display our own content.

Modify the `<Root>` component in the `/packages/my-first-theme/src/index.js` file so that it returns an `<h1>` element containing the text “Hello Frontity".

```jsx
// File: /packages/my-first-theme/src/index.js

const Root = () => {
  return (
    <>
      <h1>Hello Frontity</h1>
    </>
  )
}
```

> Webpack watches for changes in the `/packages` directory and refreshes the browser if it detects any changes. Since we have changed the content of a file within the `/packages` directory the content in the browser should automatically update.

It would be convenient, and make our codebase cleaner and more logical, if all our React components were placed together in a single directory, so let's move the `<Root>` component into its own file.

Create a new directory called `components` inside `/packages/my-first-theme/src`. This is where we will create all the component files for our theme. Then, inside `/packages/my-first-theme/src/components` create a new file called `index.js`.

Add the following code to the new file _(which we will henceforth refer to as the 'root component' file to distinguish it from the other `index.js` file in the `src` folder one level below in the structure)_. You will see that this is the same `<Root>` component as before but moved into the new file and then exported. We also need to import React into our new file.

```jsx
// File: /packages/my-first-theme/src/components/index.js

import React from "react"

const Root = () => {
  return (
    <>
      <h1>Hello Frontity</h1>
    </>
  )
}

export default Root
```

We now need to import the component into the file `/packages/my-first-theme/src/index.js` which you can modify as follows:

```jsx
// File: /packages/my-first-theme/src/index.js

import Root from "./components"

const myFirstTheme = {
  name: "my-first-theme",
  roots: {
    theme: Root,
  },
  state: {
    theme: {},
  },
  actions: {
    theme: {},
  },
}

export default myFirstTheme
```

Save both files and check that everything is still working in the browser.
