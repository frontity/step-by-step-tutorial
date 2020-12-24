# Add support for custom post types

In order to use custom post types in our project we need to add support for our custom post type in `frontity.settings.js`. We can do this by locating the object for `@frontity/wp-source` in the `packages` array and adding the `postTypes` property to `state.source`.

The `postTypes` property takes an array of objects as it's value, with each object in the array defining a distinct post type. We're only defining one post type, namely `destinations`, so we only add one object to the array.

```jsx
// File: /frontity.settings.js

// ...
{
  "name": "@frontity/wp-source",
  "state": {
    "source": {
      "url": "https://test.frontity.org",
      "postTypes": [
        {
          type: "destinations",
          endpoint: "destinations",
          archive: "/destinations"
        }
      ]
    }
  }
}
// ...
```

{% hint style="info" %}
The properties of this object are:

| Property   | Definition                                                                                                                                                                            |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`     | the CPT name, defined by the WordPress function `register_post_type()`                                                                                                                |
| `endpoint` | this will usually be the same as `type` unless the `args` array passed to `register_post_type()` specifies something different                                                        |
| `archive`  | this is needed if you want to list all the posts of that post type, note that the `args` array passed to `register_post_type()` must include `'has_archive' => true` for this to work |

Learn more in [the docs for @frontity/wp-source](https://docs.frontity.org/api-reference-1/wordpress-source#custom-post-types).
{% endhint %}

Frontity now knows about this CPT and will just work with it. Try it! Enter `localhost:3000/destinations` into your browser's address bar and you should see a listing of our favourite travel destinations. Click on one and it displays using the `<Post>` component.

**And that's it** - that's all we need to do to have our project use WordPress CPTs!

However, in the case of this CPT we don't want to display the author and date information so let's tell our `<Root>` component to use the `<Page>` component instead for this post type.

If we take a look at the data for one of the CPT URLs we can see that it has a boolean `isDestinations` property that we can utilise for this purpose.

<p>
  <img alt="Frontity in the console" src="../assets/part6img1.png">
</p>

So let's extend our `<Switch>` component to tell it to use the `<Page>` component if this value is `true`.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
<Main>
  <Switch>
    <List when={data.isArchive} />
    <Page when={data.isPage} />
    <Post when={data.isPost} />
    <Page when={data.isDestinations} />
  </Switch>
</Main>

// ...
```

To finish off let's make this accessible from our menu.

```jsx
// File: /packages/my-first-theme/src/components/index.js

// ...
<Menu>
  <Link link="/">Home</Link>
  <Link link="/destinations">Destinations</Link>
  <Link link="/about-us">About Us</Link>
</Menu>

// ...
```
