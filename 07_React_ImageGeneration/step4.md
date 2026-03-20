# Step 4: Implement the `Loader` Component

This new component is a functional React component designed to display a loading indicator as a simple and reusable way to provide feedback to users during asynchronous operations.

- It uses the `Spinner` component from the `react-bootstrap` library to provide a responsive animation. 
- It is useful for indicating to users that a background process (generating an image) is in progress.

1. Add a new file in the `src/components` folder named `Loader.js`.

2. Add the following code:

```javascript
import React from 'react';
import { Spinner } from 'react-bootstrap';

export default function Loader() {
  return (
    <div className="text-center my-3">
      <Spinner animation="border" role="status" />
      <div className="mt-2 text-muted">Generating image...</div>
    </div>
  );
}
```

## Explanation

- The outermost element is a `div` with the classes `text-center` and `my-3` for horizontal centering and vertical spacing around the loader.
- Inside this container, the `Spinner` component is rendered.
- The `animation` property specifies the spinner style (`border`, a rotating border).
- The `role="status"` attribute improves accessibility by signaling to assistive technologies that this element represents a status indicator.
- Below the spinner, another `div` displays the message `Generating image...`.
- The message uses `mt-2` to add space above the text and `text-muted` to show secondary emphasis.

[< Previous Step](step3.md) | Step 4 | [Next Step >](step5.md)
