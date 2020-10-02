# Display the list of posts

> *__[TO DO]__ modify this text to suit new context.*

> *__[TO DO]__ explain the “two-step” access to data.*

In order to display the list of posts, create a component called `<List>` in a new file `list.js`.  This will show the information in `state.source.data`, namely the `type`, `id` and `link` of each post.

```jsx
// File: /packages/jsnation-theme/src/theme-files/list.js

import React from "react";
import { connect } from "frontity";

const List = ({ state }) => {
  const data = state.source.get(state.router.link);

  return (
    <div>
      {data.items.map(item => {
        return (
          <div key={item.id}>
            {item.type} – {item.id} – {item.link}
          </div>
        );
      })}
    </div>
  );
};

export default connect(List);
```

We need to import it into our root component and use it.

```jsx
// File:  /packages/jsnation-theme/src/theme-files/index.js

// ...
import List from "./list";

const Root = ({ state }) => {
  const data = state.source.get(state.router.link);

  return (
    <>
      {/* ... */}
      <main>
        {data.isArchive && <List />}
        {data.isPost && <div>This is a post</div>}
        {data.isPage && <div>This is a page</div>}
      </main>
    </>
  );
};
```

And now let's change the `<List>` component to use the information about each of the posts to show the title and turn it into a link. Remember to import the `<Link>` component into `list.js`!

```jsx
// File: /packages/jsnation-theme/src/theme-files/list.js

import  React  from  " react " ;
import { connect } from  " frontity " ;
import  Link  from  " ./link " ;

const  List  = ({ state }) => {
   const  data  =  state.source.get(state.router.link );

  return (
    < div >
       { data.items.map( item => {
         const post = state.source.post[item.id]
         return (
           <Link key={item.id} href={post.link}>
              {post.title.rendered}
           </Link>
         );
      }) }
    </ div >
  );
};
```