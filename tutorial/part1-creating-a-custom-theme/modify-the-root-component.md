# Modify the `<Root>` component

> **[TO DO]** modify this text to suit new context.

> **[TO DO]** change folder from 'theme-files' to 'components' - de facto standard for React projects.

Let's start by modifying the `<Root>` component in the `/packages/jsnation-theme/src/index.js` file so that it returns a `<h1>` containing the text “Frontity Workshop”.

```jsx
// File: /packages/jsnation-theme/src/index.js

const Root = () => {
  return (
    <>
      <h1>Frontity Workshop</h1>
    </>
  );
};
```

The content in the browser should automatically update as we have changed a file within the `/packages` folder.

Now, let's move the <Root> component into its own file.

Create a new folder called `theme-files` inside `/packages/jsnation-theme/src`. This is where we will create all the component files for our theme. Then, inside `/packages/jsnation-theme/src/theme-files` create a new file called `index.js`.

Add the following code to the new file *(which we will henceforth refer to as the 'root component' file)*.

```jsx
// File: /packages/jsnation-theme/src/theme-files/index.js

import React from "react";

const Root = () => {
  return (
    <>
      <h1>Frontity Workshop</h1>
    </>
  );
};

export default Root;
```

We now need to import it into the file `/packages/jsnation-theme/src/index.js` which you can modify as follows:

```jsx
// File: /packages/jsnation-theme/src/index.js

import Root from "./theme-files";

const jsNationTheme = {
  name: "jsnation-theme",
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

export default jsNationTheme
```

Save both files and check that everything is still working in the browser.