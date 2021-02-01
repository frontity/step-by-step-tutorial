# Other things to do

By this stage you have a fully-functioning and full-featured Frontity site with a custom theme, and your knowledge of working with Frontity has progressed by leaps and bounds.

You're undoubtedly keen to try out your new Frontity dev skills, so here are some ideas for other features that can be added to the theme that we've been working on. Try some of them out on your own and see how you get on.

{% hint style="info" %}
☝️ Remember that you can always ask in the [Frontity community forum](https://community.frontity.org/) if you get stuck whilst working on any of these ideas. You'll find a friendly community of developers who are happy to help out and answer any questions you might have.
{% endhint %}

#### 1. Show the post excerpt on the listing pages

At the moment the listing pages just show the title of the post as a clickable link. Why not show the excerpt below each post title and style it to suit the rest of the site. How about adding a 'Read more...' link after each excerpt.

{% hint style="info" %}
**HINT** &mdash; The excerpt can be retrieved from the state in the same way that the post content is. It is available at _`{post}`_`.excerpt.rendered`.
{% endhint %}

#### 2. Display the destination CPT listing differently from the standard posts

Currently the destination CPT lists posts in the same way as the normal posts. Since it's a different type of content it would be nice if the listing displayed differently. Bear in mind that this list will always be limited so you don't need the pagination.

{% hint style="info" %}
**HINT** &mdash; You will need to modify `list.js`. You could check for the truthiness of the `isDestinationsArchive` property and return different content, or differently styled content, if it's true.
{% endhint %}

### 3. Use a single component for both posts and pages

You will recall that during the tutorial we created separate `<Post>` and `<Page>` components in separate `post.js` and `page.js` files so that posts and pages can be displayed differently. This was useful for learning purposes, but is not optimal. A single component can handle both cases.

Refactor that part of the project to dispense with the `<Page>` component, and so that the `<Post>` component handles both posts and pages.

{% hint style="info" %}
**HINT** &mdash; The `<Post>` component should conditionally check the `isPost` property and displays the posted date and author information only if it is true. If it is not true but `isPage` is true then this additional information should not be displayed.

You will also need to modify the `<Switch>` in the root component as the `<Page>` component will no longer exist.
{% endhint %}

#### 4. Create a destination component to display the custom post type differently

The destination CPT currently uses the `<Page>` component to render it's content. Create a new component that displays destinations differently.

{% hint style="info" %}
**HINT** &mdash; Remember that you will need to change `index.js` to load your new component when `data.isDestinations` is true.
{% endhint %}

#### 5. Show the featured image

At the moment we're not showing any featured images in our site, so our site lacks some visual interest. Try showing the featured image on the single post page or even on the listing page.

{% hint style="info" %}
**HINT** &mdash; The post data has a `featured_media` property. This contains the ID of the featured image for that post. You can then retrieve the data pertaining to the image in `state.source.attachment[{id}]`, including the `link` and `source_url` properties.
{% endhint %}

#### 6. Display the destination listing by region

The destinations CPT has a custom taxonomy called 'regions'. Display the destinations by region using this custom taxonomy. Currently the values available are 'Africa', 'Americas' and 'Europe'.

{% hint style="info" %}
**HINT** &mdash; You will need to add the configuration for the custom taxonomy to `frontity.settings.js` - see [the documentation here](https://docs.frontity.org/api-reference-1/wordpress-source#state-source-taxonomies). You should then update `list.js`, or at least the part of it that you implemented in 2 above.
{% endhint %}
