## Step 9: Modify the `PostList` Component

Update `PostList.js` to support editing by adding a new `onEdit` prop and rendering an `Edit` button for each post. Replace the existing code with the following one:

```javascript
import React from 'react';

export default function PostList({ posts, onEdit }) {
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
            <button onClick={() => onEdit(post)} style={{ marginRight: '1rem' }}>
              Edit
            </button>
          </div>
        ))
      )}
    </div>
  );
}
```

[< Previous Step](step8.md) | Step 9 | [Next Step >](step10.md)
