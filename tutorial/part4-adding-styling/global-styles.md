# Global Styles

The first thing we will do is create global styles. These apply site-wide and should be added to the root component of your theme. We'll change the font to be sans-serif. To do this import the `<Global>` component and the `css` function from Frontity into our root component.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
import { connect, Global, css } from "frontity";

const Root = ({ state }) => {

  const data = state.source.get(state.router.link);

  return (
    <>
      <Global
        styles={css`
          html {
            font-family: system-ui, Verdana, Arial, sans-serif;
          }
        `}
      />
      {/* ... */}
    </>
  );
};
```

The `css` function takes as it's argument a [tagged template literal](https://wesbos.com/tagged-template-literals), which in this case consists of standard CSS contained within backticks. These styles are applied to the `styles` attribute on the `Global` component. When you save the file you should notice that the fonts on your site have changed automatically.

Next we'll look at the power and flexibility that styled components give us.