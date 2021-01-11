# Other things to do

> _**TODO**: provide hints and tips and links to the docs for each suggestion_

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

#### 3. Create a destination component to display the custom post type differently

The destination CPT currently uses the `<Page>` component to render it's content. Create a new component that displays destinations differently.

{% hint style="info" %}
**HINT** &mdash; Remember that you will need to change `index.js` to load your new component when `data.isDestinations` is true.
{% endhint %}

#### 4. Show the featured image

At the moment we're not showing any featured images in our site, so our site lacks some visual interest. Try showing the featured image on the single post page or even on the listing page.

{% hint style="info" %}
**HINT** &mdash; The post data has a `featured_media` property. This contains the ID of the featured image for that post. You can then retrieve the data pertaining to the image in `state.source.attachment[{id}]`, including the `link` and `source_url` properties.
{% endhint %}

#### 5. Display the destination listing using the 'regions' custom taxonomy

> _**TODO**: provide hints and tips and links to the docs_
