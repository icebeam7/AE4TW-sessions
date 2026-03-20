## Step 6: Implement a list of posts (Part 2) by including the `PostList` Component in `App.js`

In this step, you connect the `App` component with the API and render the `PostList` component.

1. In `src/App.js`, import **React hooks** and the custom component:

```javascript
import React, { useState, useEffect } from 'react';
import PostList from './components/PostList';
```

> **React Hooks**, introduced in React 16.8, enable functional components to use state, lifecycle, and other React features without relying on class components.

2. Create a constant with the API base URL:

```javascript
const API_URL = 'https://jsonplaceholder.typicode.com/posts';
```

> This variable stores the base url of an API that brings a list of posts

3. Inside the `App` function, create state for posts (before `return`):

```javascript
const [posts, setPosts] = useState([]);
```

> - The `posts` constant is bound to a `setPosts` function.
> - When the `setPosts` function is invoked, its argument is assigned to the `posts` constant.
> - The `useState` hook is used to define the state variable (posts), initialized as an **empty array**.
> - This state will hold the list of posts fetched from the API. 

4. Use `useEffect` to fetch 5 posts when the component first renders:

```javascript
  useEffect(() => {
    fetch(API_URL + '?_limit=5')
      .then((res) => res.json())
      .then((data) => setPosts(data))
      .catch((err) => console.error('Error fetching posts:', err));
  }, []);
```

> - The `useEffect` hook sends a request to the API with a `_limit` parameter.
> - The request returns data from the API **when the component is first rendered**.
> - The data includes a collection of `5` posts, which are stored in the `posts` state by calling the `setPosts` function. 

5. Replace the `return` section with:

```javascript
  return (
    <div className="App" style={{ padding: '2rem' }}>
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
      </header>
      <main>
        <h1>List of Posts</h1>
        <PostList posts={posts} />
      </main>
    </div>
  );
```

> - You are setting a heading level 1 and rendering the `PostList` custom component 
> - You are passing the `posts` state as a property.
> - This component is responsible for displaying the fetched posts.

6. Save `App.js`.

[< Previous Step](step5.md) | Step 6 | [Next Step >](step7.md)
