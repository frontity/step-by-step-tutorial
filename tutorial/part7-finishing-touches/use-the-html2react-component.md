# Use the `<html2react>` component

Problem with internal links, e.g. in post "Latest Trip to India". The link to "New7Wonders of the World" at the bottom of the post forces SSR and a page reload. Another example in post "Shinjuku Gyoen National Garden" and the link "post about the Banff National Park".

We'll use `<html2react>` component to process our content and replace any links with the `<Link>` component that we import into our `<Root>` component.

`"@frontity/html2react"` should already be in `frontity.settings.js`

Add this to root level `index.js`

```jsx
import link from "@frontity/html2react/processors/link";

// ...
libraries: {
    html2react: {
      processors: [link]
    }
  }
```

In post.js and page.js change

```jsx
<div dangerouslySetInnerHTML={{ __html: post.content.rendered }} />
```

to

```jsx
const Html2React = libraries.html2react.Component;

// ...
<Html2React html={post.content.rendered} />
```

don't forget to pass `libraries` to the component.