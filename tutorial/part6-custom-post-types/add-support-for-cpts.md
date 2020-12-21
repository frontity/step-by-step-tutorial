# Add support for custom post types

> _**[TO DO]** new content to be written._

As you will already be aware, our example source data is a travel blog. We have implemented a Custom Post Type (CPT) in WordPress for our favourite destinations. This CPT is called... "destinations" - what else?!

The first thing we need to do is to add support for our custom post type in`frontity.settings.js`. Add the `postTypes` property to `state.source`. This takes an array of objects as it's value, with each object in the array defining a post type. We're only defining one post type, namely `destinations` so we only add one object to the array.

The properties of this object are:

- `type` - the CPT name, defined by the WordPress function `register_post_type()`;
- `endpoint` - this will usually be the same as `type` unless the `args` array passed to `register_post_type()` specifies something different;
- `archive` - this is needed if you want to list all the posts of that post type, note that the `args` array passed to `register_post_type()` must include `'has_archive' => true` for this to work.

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

Frontity now knows about this CPT and will just work with it. Try it! Enter `localhost:3000/destinations` into your browser's address bar and you should see a listing of our favourite travel destinations. Click on one and it displays using the `<Post>` component.

In the case of this CPT we don't want to display the author and date information so let's tell our `<Root>` component to use the `<Page>` component instead for this post type.

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
