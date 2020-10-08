# Add pagination

> *__[TO DO]__ modify this text to suit new context.*

> *__[TO DO]__ images may need updating.*

Click on the `More posts` link in the menu to navigate to `/page/2` and examine `frontity.state` in the console. You will notice that the data for the page has both `previous` and `next` properties.

<p>
  <img alt="Frontity in the console" src="../assets/console-5.png" width="700">
</p>

We can use these properties to add pagination to our `<List>` component. We will add a `<PrevNextNav>` component to style two buttons that enable us to page through the lists of posts.

Change `list.js` as follows.

```jsx
// File: /packages/my-first-theme/src/theme-files/list.js

import React from "react"
import { connect, styled } from "frontity"
import Link from "./link"

const List = ({ state, actions }) => {
    const data = state.source.get(state.router.link)

    return (
        <Items>
            { data.items.map( item => {
                const post = state.source.post[item.id]
                return (
                    <Link key={item.id} href={post.link}>
                        {post.title.rendered}
                    </Link>
                )
            })}
            <PrevNextNav>
                {
                    data.previous && <button onClick={ () => {
                        actions.router.set(data.previous)
                    } }>
                        &#171; Prev
                    </button>
                }
                {
                    data.next && <button onClick={ () => {
                        actions.router.set(data.next)
                    } }>
                        Next &#187;
                    </button>
                }
            </PrevNextNav>
        </Items>
    )
}

export default connect(List)

const Items = styled.div`
    & > div {
        margin: 12px 0;
        font-size: 1.2em;
    }
`
const PrevNextNav = styled.div`

    padding-top: 1.5em;

    & > button {
        background: #eee;
        text-decoration: none;
        padding: 0.5em 1em;
        color: #888;
        border: 1px solid #aaa;
        font-size: 0.8em;
        margin-right: 2em;
    }
    & > button:hover {
        cursor: pointer;
    }
`
```

We've included conditional checks so that the 'Previous' button doesn't show on the first page and the 'Next' button doesn't show on the last page, as they're not needed in those locations.