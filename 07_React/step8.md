## Step 8: Implement Addition and Edition of Posts

In this step, you create a `PostForm` component to add and edit posts.

1. In `src/components`, create a new file named `PostForm.js`.

2. Import React hooks [in the same way you did before](step6.md).

3. Define and export the component with `onSubmit` and `editingPost` props:

```javascript
export default function PostForm({ onSubmit, editingPost }) {

}
```

- `onSubmit`: Callback executed when the form is submitted.
- `editingPost`: Optional post object used to pre-fill the form in edit mode.

4. Inside the component, define state variables:

```javascript
const [title, setTitle] = useState('');
const [body, setBody] = useState('');
```

> These hold the values of the form’s input fields and will be managed using the `useState` hook.

5. Add `useEffect` to switch between add and edit modes:

```javascript
useEffect(() => {
  if (editingPost) {
    setTitle(editingPost.title);
    setBody(editingPost.body);
  } else {
    setTitle('');
    setBody('');
  }
}, [editingPost]);
```

> - If `editingPost` is provided, the `title` and `body` states are populated with the corresponding values from the post being edited.
> - On the other hand, if `editingPost` is `null` or `undefined`, the form fields are reset to empty strings.
> - This ensures the form behaves correctly when switching between **add** and **edit** modes.

6. Form submission: A `handleSubmit` function is triggered when the form is submitted. It prevents the default form submission behavior using `e.preventDefault()`. A post object is created with the following properties: `id`, `title`, `body`, `userID`. Add a submit handler:

```javascript
const handleSubmit = (e) => {
  e.preventDefault();
  const post = {
    id: editingPost?.id || Math.random(),
    title,
    body,
    userId: 1,
  };
  onSubmit(post);
  setTitle('');
  setBody('');
};
```

> The `onSubmit` callback will be called with the post object. After submission, the form fields are cleared by resetting `title` and `body` to empty strings.

7. Render the form UI:

```javascript
return (
  <form onSubmit={handleSubmit} style={{ marginBottom: '2rem' }}>
    <h2>{editingPost ? 'Edit Post' : 'Add Post'}</h2>
    <input
      type="text"
      placeholder="Title"
      value={title}
      required
      onChange={(e) => setTitle(e.target.value)}
      style={{ display: 'block', marginBottom: '1rem', width: '100%' }}
    />
    <textarea
      placeholder="Body"
      value={body}
      required
      onChange={(e) => setBody(e.target.value)}
      style={{ display: 'block', marginBottom: '1rem', width: '100%' }}
    />
    <button type="submit">{editingPost ? 'Update' : 'Add'} Post</button>
  </form>
);
```

> Rendering: The content that will be displayed in the component goes inside a return block. It defines a form which includes:
> - A heading level 2 with the content "Edit Post" or "Add Post" based on whether `editingPost` is provided.
> - Two input fields: A text input for the post's title and a textarea for the post's body. Both fields are controlled components, meaning their values are tied to the component's state (title and body).
> - A submit button with the text "Update Post" or "Add Post" based on `editingPost`.


[< Previous Step](step7.md) | Step 8 | [Next Step >](step9.md)
