# Formatting the date

When you view a post you may notice that the date is not formatted in an easy to read way.

<p>
  <img alt="Frontity in the browser" src="../assets/part3img7.png">
</p>

Let's fix that now. Doing this gives us the opportunity to use an external library with Frontity. This is something that you're likely to need to do in real-world project development, so it's well worth covering here.

We're going to use [Day.js](https://day.js.org/) to format our date string.

You can install Day.js by entering the following line into the terminal:

```
npm install dayjs
```

If you check the `package.json` file in the root of your project folder you will now see that `dayjs` has been added as a dependency.

<p>
  <img alt="Dependencies in package.json" src="../assets/part3img8.png">
</p>

Next, let's import Day.js into our `post.js` file:

```jsx
// File: /packages/my-first-theme/src/components/post.js
import React from "react";
import { connect } from "frontity";
import dayjs from 'dayjs'
// ...
```

We now need to create a Day.js object and we pass in `post.date`, which is the date string that is currently displaying in our post. We can do that with `dayjs(post.date)`, and we then call the `format` function of the `dayjs` object passing it a formatting string.

We'll store the result in a variable (which we'll call `formattedDate`) for later use.

```jsx
// File: /packages/my-first-theme/src/components/post.js

// ...
    const formattedDate = dayjs(post.date).format('DD MMMM YYYY');
// ...
```

See the [Day.js documentation](https://day.js.org/docs/en/display/format) for other possible formatting strings. For example, try replacing `DD MMMM YYYY` above with `MMM DD, YYYY` or `DD-MM-YY` to see how the appearance of the date changes.

Your `post.js` file should now look like this:

```jsx
// File: /packages/my-first-theme/src/components/post.js
import React from "react";
import { connect } from "frontity";
import dayjs from 'dayjs'

const Post = ({ state }) => {

  const data = state.source.get(state.router.link);
  const post = state.source[data.type][data.id];
  const author = state.source.author[post.author];

  const formattedDate = dayjs(post.date).format('DD MMMM YYYY');

  return (
    <div>
      <h2>{post.title.rendered}</h2>
      <p><strong>Posted: </strong>{formattedDate}</p>
      <p><strong>Author: </strong>{author.name}</p>
      <div dangerouslySetInnerHTML={{ __html: post.content.rendered }} />
    </div>
  );

};

export default connect(Post);
```

Our date is now formatted in a much more pleasing way.

<p>
  <img alt="Frontity in the browser" src="../assets/part3img9.png">
</p>