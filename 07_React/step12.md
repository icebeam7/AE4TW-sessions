## Step 12: Handle Deletion of Information

1. In `PostList.js`, include a new callback property named `onDelete`.

2. Add a `Delete` button that calls `onDelete(post.id)`:

```javascript
export default function PostList({ posts, onEdit, onDelete }) {
  // ...
  return (
    <div>
      {/* ... */}
      <button onClick={() => onDelete(post.id)}>Delete</button>
    </div>
  );
}
```

3. In `App.js`, add `deletePost` which deletes an existing post on the server and removes it from the app’s local state (posts):


```javascript
const deletePost = async (id) => {
  await fetch(`${API_URL}/${id}`, { method: 'DELETE' });
  setPosts(posts.filter((p) => p.id !== id));
};
```

4. Pass `deletePost` to `PostList`:

```javascript
<PostList
  posts={posts}
  onEdit={setEditingPost}
  onDelete={deletePost}
/>
```

5. Save all your work.

6. Test the app again (if it's running, press `Ctrl-C` to stop the server first:

- Verify the initial list appears.

<img width="1790" height="1526" alt="image" src="https://github.com/user-attachments/assets/87dfbc69-3cef-4f5d-a4d5-b52c2af62237" />

- Delete the first post and confirm it is removed from the UI.

<img width="1790" height="1526" alt="image" src="https://github.com/user-attachments/assets/c351ad51-7e55-40a9-90d7-5acc8aa04b27" />

[< Previous Step](step11.md) | Step 12
