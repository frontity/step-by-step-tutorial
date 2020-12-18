# Formatting the date

When you view a post you may notice that the date is not formatted in an easy to read way.

<p>
  <img alt="Frontity in the browser" src="../assets/part3img14.png">
</p>

Let's fix that now. Doing this gives us the opportunity to use an external library with Frontity. Installing and using external JavaScript libraries is something that you're likely to need to do in real-world project development, so it's well worth covering here.

Frontity will happily work with almost any package available on [npmjs.com](https://www.npmjs.com/). There are a number of packages for formatting dates, probably the best known of which is [Moment](https://momentjs.com/.). However, Moment is a large package so in the interests of streamlining our project as much as possible we're instead going to use the more lightweight [Day.js](https://day.js.org/) to format our date string.

{% hint style="info" %}
If, like us, you prefer to keep your bundle sizes as small as possible [bundlephobia.com](https://bundlephobia.com/) is a great resource for finding alternatives to large and heavyweight npm packages.
{% endhint %}

Open your terminal and ensure that you're in the root directory of your project. You can then install Day.js by running the following command:

```
npm install dayjs
```

If you check the `package.json` file in the root of your project folder you will now see that `dayjs` has been added as a dependency.

<p>
  <img alt="Dependencies in package.json" src="../assets/part3img15.png">
</p>

Next, since the `<Post>` component is the only one that's going to use it, let's import Day.js into our `post.js` file:

```jsx
// File: /packages/my-first-theme/src/components/post.js
import React from "react"
import { connect } from "frontity"
import dayjs from "dayjs"
// ...
```

We now need to create a Day.js object and we pass in `post.date`, which is the tricky to read date string that is currently displaying in our post. We can do that with `dayjs(post.date)`, and we then call the `format` function of the `dayjs` object passing it a formatting string.

We'll store the result in a variable (which we'll call `formattedDate`) for later use.

```jsx
// File: /packages/my-first-theme/src/components/post.js

// ...
const formattedDate = dayjs(post.date).format("DD MMMM YYYY")
// ...
```

See the [Day.js documentation](https://day.js.org/docs/en/display/format) for other possible formatting strings. For example, try replacing `DD MMMM YYYY` above with `MMM DD, YYYY` or `DD-MM-YY` to see how the appearance of the date changes. Use your preferred formatted version.

We'll also use the `formattedDate` variable holding our formatted date in our display by replacing `post.date` with it.

Your `post.js` file should now look like this:

```jsx
// File: /packages/my-first-theme/src/components/post.js
import React from "react"
import { connect } from "frontity"
import dayjs from "dayjs"

const Post = ({ state }) => {
  const data = state.source.get(state.router.link)
  const post = state.source[data.type][data.id]
  const author = state.source.author[post.author]

  const formattedDate = dayjs(post.date).format("DD MMMM YYYY")

  return (
    <div>
      <h2>{post.title.rendered}</h2>
      <p>
        <strong>Posted: </strong>
        {formattedDate}
      </p>
      <p>
        <strong>Author: </strong>
        {author.name}
      </p>
      <div dangerouslySetInnerHTML={{ __html: post.content.rendered }} />
    </div>
  )
}

export default connect(Post)
```

Our date is now formatted in a much more pleasing way.

<p>
  <img alt="Frontity in the browser" src="../assets/part3img16.png">
</p>
