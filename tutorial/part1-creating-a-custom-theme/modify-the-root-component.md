# Modify the `<Root>` component

> *__[TO DO]__ modify this text to suit new context.*

> *__[TO DO]__ change folder from 'components' to 'components' - de facto standard for React projects.*

Let's start by modifying the `<Root>` component in the `/packages/my-first-theme/src/index.js` file so that it returns a `<h1>` containing the text “Hello Frontity".

```jsx
// File: /packages/my-first-theme/src/index.js

const Root = () => {
  return (
    <>
      <h1>Hello Frontity</h1>
    </>
  );
};
```

The content in the browser should automatically update as we have changed a file within the `/packages` folder.

Now, let's move the <Root> component into its own file.

Create a new folder called `components` inside `/packages/my-first-theme/src`. This is where we will create all the component files for our theme. Then, inside `/packages/my-first-theme/src/components` create a new file called `index.js`.

Add the following code to the new file *(which we will henceforth refer to as the 'root component' file)*.

```jsx
// File: /packages/my-first-theme/src/components/index.js

import React from "react";

const Root = () => {
  return (
    <>
      <h1>Hello Frontity</h1>
    </>
  );
};

export default Root;
```

We now need to import it into the file `/packages/my-first-theme/src/index.js` which you can modify as follows:

```jsx
// File: /packages/my-first-theme/src/index.js

import Root from "./components";

const myFirstTheme = {
  name: "my-first-theme",
  roots: {
    theme: Root
  },
  state: {
      theme: {}
  },
  actions: {
      theme: {}
  }
};

export default myFirstTheme
```

Save both files and check that everything is still working in the browser.