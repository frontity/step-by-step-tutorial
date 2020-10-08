# Add dynamic styling

> *__[TO DO]__ modify this text to suit new context.*

> *__[TO DO]__ add more explanation and another example here.*

CSS-in-JS allows us to modify the styling of elements dynamically. Let's take a look at how we can do this.

You will recall that we added an 8px wide border to the bottom of our header. We'll use that to indicate whether we're on a `list` page, a `post` page, or a `page`, erm..., page 🤷🏻‍♂️ by changing the colour of the border.

To do this we add a prop to the `<Header>` component.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
<Header isPostType={data.isPostType}>
// ...
```

This prop gets passed to a function that we add to our CSS that conditionally checks the boolean value passed in to determine what colour the border should be, i.e. either green in the case of a `post` or `page`, or maroon in the case of a `list`. We're no longer using JSX here so we need to prepend the function with a $ sign, and we also need to use the ternary operator - we cannot use `if...then...else` in JavaScript embedded within a template literal.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
const Header = styled.header`
  background-color: #eee;
  border-width: 0 0 8px 0;
  border-style: solid;
  border-color: ${ props => props.isPostType ? : 'lightseagreen' : 'maroon'};
`
```

Let's extend this to get a different colour for pages.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
<Header isPostType={data.isPostType} isPage={data.isPage}>
// ...

// ...
const Header = styled.header`
  background-color: #eee;
  border-width: 0 0 8px 0;
  border-style: solid;
  border-color: ${ props => props.isPostType ? props.isPage ? 'lightsteelblue' : 'lightseagreen' : 'maroon'};
`
```

Awesome, our site is starting to look pretty good now! 👌