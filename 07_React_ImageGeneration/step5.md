# Step 5: Implement the ImageDisplay Component

This component is a functional React component designed to display an image.

- It uses the `Image` component from the `react-bootstrap` library to ensure the image is styled responsively with accessibility considerations.

1. Add a new file in the `src/components` folder named `ImageDisplay.js`.

2. Add the following code:

```javascript
import React from 'react';
import { Image } from 'react-bootstrap';

export default function ImageDisplay({ url }) {
  return (
    <div className="text-center">
      <Image src={url} alt="AI Generated" fluid rounded className="shadow" />
    </div>
  );
}
```

## Explanation

- The component accepts a single prop, `url`, which is the URL of the image to be displayed.
- This URL is passed to the `src` attribute of the `Image` component.
- The outermost `div` centers the image horizontally within its container.
- Inside this container, the `Image` component is rendered with additional props and classes:
- The `alt` attribute is set to `AI Generated`, providing descriptive alternative text for accessibility.
- The `fluid` prop ensures the image scales responsively to fit its container on different screen sizes.
- The `rounded` prop applies rounded corners to the image.
- The `className="shadow"` adds a subtle shadow effect around the image.


[< Previous Step](step4.md) | Step 5 | [Next Step >](step6.md)
