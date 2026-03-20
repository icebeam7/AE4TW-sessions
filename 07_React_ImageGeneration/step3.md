# Step 3: Implement the ImageGeneratorForm Component

In this step, you will create a functional, reusable React component designed to render a simple form for generating images based on user input. It will allow users to enter a description and trigger an action with a button click.

The component uses `react-bootstrap` for responsive design and ensures that the input field and button are well-aligned and accessible.

The component accepts three properties:

- `prompt`
- `setPrompt`
- `onGenerate`

`react-bootstrap` components should be imported individually (for example, `react-bootstrap/Button`) rather than importing the entire library. Doing so pulls in only the specific components you use, which can significantly reduce the amount of code sent to the client.

1. In the `src` folder, create a new folder named `components`.

2. Inside `components`, create a new file named `ImageGeneratorForm.js`.

3. Add the following code to the new file and save it:

```javascript
import React from 'react';
import { Form, Button, Row, Col } from 'react-bootstrap';

export default function ImageGeneratorForm({ prompt, setPrompt, onGenerate }) {
  return (
    <Form className="mb-3">
      <Row className="justify-content-center">
        <Col md={6}>
          <Form.Control
            type="text"
            value={prompt}
            onChange={(e) => setPrompt(e.target.value)}
            placeholder="Describe your image..."
          />
        </Col>
        <Col md="auto">
          <Button onClick={onGenerate} variant="primary">
            Generate
          </Button>
        </Col>
      </Row>
    </Form>
  );
}
```

## Explanation

- The `Form` element serves as the container for the input and button elements. It uses the `mb-3` class to add a margin at the bottom.
- Inside the form, a `Row` with the `justify-content-center` class is used to center the content horizontally.
- The row contains two `Col` components for responsive structure:
- The first column (`Col md={6}`) contains a `Form.Control` input field.
- This input is bound to the `prompt` prop via the `value` attribute, so it reflects the current prompt state.
- The `onChange` handler updates the prompt state by calling `setPrompt`.
- The `placeholder` attribute gives users guidance: `Describe your image...`.
- The second column (`Col md="auto"`) contains a `Button` component.
- The button uses `variant="primary"` for styling and triggers `onGenerate` when clicked, which handles image generation logic.

[< Previous Step](step2.md) | Step 3 | [Next Step >](step4.md)
