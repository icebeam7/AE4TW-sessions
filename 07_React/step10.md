## Step 10: Modify `App.js`

Now update `App.js` to support creating and editing posts.

1. Import `PostForm` in a similar way you did for `PostList` component: 

2. Add state for edit mode inside `App`. A new state variable (`editingPost`) is bound to a `setEditingPost` function. When the function is invoked, its argument is assigned to `editingPost`. The `useState` hook is used to define the state variable, initialized with `null` value. This state will hold the mode (edition or new):

```javascript
  const [editingPost, setEditingPost] = useState(null);
```

3. Define an `addPost` asynchronous function. It will be responsible for adding a new post to the app by sending it to a server and updating the local state (posts) with the new post:

```javascript
  const addPost = async (post) => {
    const res = await fetch(API_URL, {
      method: 'POST',
      headers: { 'Content-type': 'application/json' },
      body: JSON.stringify(post),
    });
    const newPost = await res.json();
    setPosts([newPost, ...posts]);
  };
```

4. Similarly, define an `updatePost` asynchronous function that updates an existing post on the server and the app’s local state (posts).

```javascript
  const updatePost = async (updatedPost) => {
    await fetch(`${API_URL}/${updatedPost.id}`, {
      method: 'PUT',
      headers: { 'Content-type': 'application/json' },
      body: JSON.stringify(updatedPost),
    });
    setPosts(posts.map((p) => (p.id === updatedPost.id ? updatedPost : p)));
    setEditingPost(null);
  };
```

> - `setPosts(posts.map(...))` replaces only the updated post while leaving all other posts unchanged.
> - The `setEditingPost` function is called with null to clear the editing state. This signals that the editing process is complete and resets any UI elements related to editing.

5. Update the JSX content returned by the `App` component by rendering the `PostForm` component and passing the `setEditingPost` state variable to the `onEdit` property in the `PostList` component:

```javascript
  return (
    <div className="App" style={{ padding: '2rem' }}>
      <h1>List of Posts</h1>
      <PostForm
        onSubmit={editingPost ? updatePost : addPost}
        editingPost={editingPost}
      />
      <PostList
        posts={posts}
        onEdit={setEditingPost}
      />
    </div>
  );
```

[< Previous Step](step9.md) | Step 10 | [Next Step >](step11.md)
