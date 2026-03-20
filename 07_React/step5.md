## Step 5: Implement a list of posts (Part 1) by creating a `PostList` Component

This step creates a **custom React component** that displays a list of posts.

1. In the `src` folder, create a new folder named `components`.

2. Inside `src/components`, create a new file named `PostList.js`.

<img width="490" height="1218" alt="image" src="https://github.com/user-attachments/assets/33053ca1-ce13-44e1-9ce0-21ec350d1842" />


3. Add the following code to `PostList.js` and save the file:

```javascript
import React from 'react';

export default function PostList({ posts }) {
  return (
    <div>
      <h2>Posts</h2>
      {posts.length === 0 ? (
        <p>No posts available.</p>
      ) : (
        posts.map((post) => (
          <div key={post.id} style={{ border: '1px solid #ccc', marginBottom: '1rem', padding: '1rem' }}>
            <h3>{post.title}</h3>
            <p>{post.body}</p>
          </div>
        ))
      )}
    </div>
  );
}
```

### What this component does

- Renders an `h2` heading with the text `Posts`.
- Shows `No posts available.` when the `posts` array is empty.
- Uses `.map()` to render one `<div>` per post when data exists.
- Displays each post title in an `h3` and body in a paragraph.
- Uses `key={post.id}` so React can efficiently update list items.

### Other important remarks:

- The component is **exported** as the default export of the file, allowing it to be imported and used in other parts of the application, such as the App component.

- The **ternary operator** (`? :`) is used to decide whether to display a `No posts available` message or the list of posts, based on the length of the `posts` array.

- The `map` method dynamically generates a list of JSX elements based on the data in the posts array. This is a common pattern in React for rendering lists.

- The `key` attribute ensures that each post's <div> is uniquely identifiable, which helps React optimize rendering and avoid unnecessary re-renders.


[< Previous Step](step4.md) | Step 5 | [Next Step >](step6.md)
