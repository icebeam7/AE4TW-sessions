# Building Accessible UI Components (Without Frameworks)

Here are the topics that will be covered today:

- Building Components using native HTML
  - Accesible Modal Dialog
  - Accordion
  - Tabs
  - Dropdown Menu

- Accessibility with ARIA (Accessible Rich Internet Applications)
  - Prefering native HTML over ARIA
  - If you use ARIA, you must manage its state
  - Everything must be keyboard accessible
  - Focus must always be visible
  - Never create keyboard traps

# Part 1 - Accessible Modal Dialog

## Important Concepts:
- Focus Traps: Keep keyboard focus locked within the modal while it’s open.
- Escape Options: Allow users to exit using the `Escape` key, a close button, or an optional backdrop click.
- ARIA Attributes: Use `role="dialog"`, `aria-modal="true"`, `aria-labelledby`, and `aria-describedby` for screen reader support.
- Keyboard Navigation: Ensure `Tab`, `Shift+Tab`, and other keys work intuitively within the modal.
- Focus Management: Shift focus to the modal on open and back to the trigger element on close.

1. Create a new HTML5 document (`accessibility.html`).

2. Add the following basic structure in the body section:

```html
<section>
  <h2>Modal Example</h2>
  <button id="openModal">Open Modal</button>
</section>

<div id="modal" role="dialog" aria-modal="true" aria-hidden="true">
  <div id="modal-content">
    <h2>Modal Title</h2>
    <p>This is an accessible modal.</p>
    <button id="closeModal">Close</button>
  </div>
</div>
```

- `role="dialog"`: Indicates that this element is a dialog, making it accessible for assistive technologies.
- `aria-modal="true"`: Specifies that the modal is a top-level dialog and prevents interaction with the rest of the page while it is open.
- `aria-hidden="true"`: Initially hides the modal from assistive technologies (it will be toggled to false when the modal is opened).

3. Create a separate CSS file (`styles.css`) and link it in your HTML file. Here's the code:

```css
body {
    font-family: sans-serif;
    line-height: 1.5;
}

button {
    padding: 0.5em 1em;
    margin: 0.2em;
}

section {
    margin: 1em 0;
}

#modal { 
    display: none; 
    position: fixed; 
    top:0; 
    left:0; 
    width:100%; 
    height:100%; 
    background: rgba(0,0,0,0.6); 
    justify-content:center; 
    align-items:center; 
}

#modal[aria-hidden="false"] { 
    display: flex; 
}

#modal-content { 
    background: #fff; 
    padding: 1em;
    max-width: 400px; 
    width: 90%; 
}
```

4. Additionally, create a JavaScript file (`script.js`). Here you will **implement focus trapping**. Moreover, this script manages the behavior of a modal dialog, ensuring accessibility and proper focus management

Read more about Focus Trap [here](https://www.uxpin.com/studio/blog/how-to-build-accessible-modals-with-focus-traps/)

```javascript
let lastFocusedElement = null;

const modal = document.getElementById("modal");
const openModalButton = document.getElementById("openModal");
const closeModalButton = document.getElementById("closeModal");

openModalButton.addEventListener("click", () => {
  lastFocusedElement = document.activeElement || null;
  modal.setAttribute("aria-hidden","false");
  const firstFocusable = modal.querySelector("button, [href], input, select, textarea, [tabindex]:not([tabindex='-1'])");
  if(firstFocusable) firstFocusable.focus();
});

closeModalButton.addEventListener("click", () => {
  modal.setAttribute("aria-hidden","true");
  if(lastFocusedElement) lastFocusedElement.focus();
});

// Trap focus inside modal
modal.addEventListener("keydown", (e) => {
  if(e.key === "Tab") {
    const focusable = Array.from(modal.querySelectorAll("button, [href], input, select, textarea, [tabindex]:not([tabindex='-1'])"));
    if(focusable.length === 0) return;
    const first = focusable[0];
    const last = focusable[focusable.length -1];
    if(e.shiftKey) { // shift+tab
      if(document.activeElement === first) {
        e.preventDefault();
        last.focus();
      }
    } else { // tab
      if(document.activeElement === last) {
        e.preventDefault();
        first.focus();
      }
    }
  } else if(e.key === "Escape") {
    closeModalButton.click();
  }
});
```

Don't forget to link it in your HTML file. Use the `defer` option.

> Deferring the script allows the browser to download it in parallel while parsing a web page, and then execute the script after the page has finished parsing.

- When the `Open Modal` button is clicked:
    - The currently focused element is saved in `lastFocusedElement`.
    - The `aria-hidden` attribute of the modal is set to `false`, making it visible to assistive technologies.
    - The first focusable element inside the modal is focused.

- When the `Close Modal` button is clicked:
    - The `aria-hidden` attribute is set to "true", hiding the modal.
    - Focus is returned to the element that was focused before the modal was opened.

- Focus trapping:
    - When the `Tab` key is pressed, the code ensures that focus stays within the modal.
      - If `Shift + Tab` is pressed and the first focusable element is active, focus loops to the last focusable element.
      - If `Tab` is pressed and the last focusable element is active, focus loops to the first focusable element.

- `Escape` key:
    - If the `Escape` key is pressed, the modal is closed by triggering the `Close Modal` button's click event.

5. Test your implementation. Review the following:

- The Modal can be opened using the keyboard.
- It closes with Escape
- Focus is trapped!

<img width="695" height="365" alt="image" src="https://github.com/user-attachments/assets/ba13e2a7-b915-4aa6-8afb-e8faf58128a5" />

# Part 2 - Accessible Accordion

Implement an **accordion**. An accordion is a UI pattern consisting of vertically stacked, collapsible content panels. Each panel has a header (title) that users click to reveal or hide detailed information. They are designed to save screen space, often used for FAQs or menus, reducing the need for extensive scrolling

1. Here is the HTML code:

```
<section class="accordion">
  <h2>Accordion Example</h2>
  <button aria-expanded="false" aria-controls="acc1">Section 1</button>
  <div id="acc1" hidden>
    <p>Content for section 1</p>
  </div>
  <button aria-expanded="false" aria-controls="acc2">Section 2</button>
  <div id="acc2" hidden>
    <p>Content for section 2</p>
  </div>
</section>
```

- Each `<button>` acts as a toggle for its corresponding content section.
- `aria-expanded="false"`: Indicates whether the section is expanded (true) or collapsed (false).
- `aria-controls="acc1"`: Links the button to the content it controls (via the id of the content <div>).

2. Now, implement the styles:

```
.accordion [hidden] { 
    display: none; 
}

.accordion button { 
    display: block; width: 100%; text-align: left; 
}
```

- `display: block;` makes the button take up the full width of its container by default.

3. Finally, here's the script code that makes the accordion work as expected:

```
document.querySelectorAll(".accordion button").forEach(btn => {
  btn.addEventListener("click", () => {
    const expanded = btn.getAttribute("aria-expanded") === "true";
    btn.setAttribute("aria-expanded", String(!expanded));
    const content = document.getElementById(btn.getAttribute("aria-controls"));
    if (content) content.hidden = expanded; // toggle hidden
  });
});
```

> The `aria-expanded` attribute is set on an element to indicate if a control is expanded or collapsed. Communicates the expanded/collapsed state of each section to assistive technologies.
> The `aria-controls` attribute links the button to the content it controls, improving navigation for screen readers.

4. Test your implementation. You will observe the following:

- The button is focusable
- `aria-expanded` updates accordingly
- Panel toggles visibility
- Works with the keyboard (Use `Enter` or `Space`)

<img width="570" height="401" alt="image" src="https://github.com/user-attachments/assets/68c50fad-f4fa-41e1-8e93-0bd52c270280" />

# Part 3 - Accessible Tabs

1. Here is the HTML code for displaying Tabs that contain inner elements:

```
<section class="tabs">
  <h2>Tabs Example</h2>
  <div role="tablist">
    <button role="tab" aria-selected="true" aria-controls="panel1" id="tab1">Tab 1</button>
    <button role="tab" aria-selected="false" aria-controls="panel2" id="tab2">Tab 2</button>
  </div>
  <div id="panel1" role="tabpanel" aria-labelledby="tab1">Content 1</div>
  <div id="panel2" role="tabpanel" aria-labelledby="tab2" hidden>Content 2</div>
</section>
```

2. Now, implement the styles for this control:

```
.tabs [role="tabpanel"][hidden] { 
    display: none; 
}

.tabs [role="tab"] { 
    cursor: pointer; 
}
```

3. Finally, here's the script code that makes the tabs work as expected:

```
const tabs = document.querySelectorAll('.tabs [role="tab"]');
const panels = document.querySelectorAll('.tabs [role="tabpanel"]');

tabs.forEach(tab => {
  tab.addEventListener('click', () => {
    tabs.forEach(t => t.setAttribute('aria-selected','false'));
    panels.forEach(p => p.hidden = true);
    tab.setAttribute('aria-selected','true');
    const panel = document.getElementById(tab.getAttribute('aria-controls'));
    if(panel) panel.hidden = false;
    tab.focus();
  });
});
```

4. Test your implementation. You will observe the following:

- Only one tab can be selected at once
- `aria-selected` updates accordingly
- Only the active panel is visible

<img width="535" height="439" alt="image" src="https://github.com/user-attachments/assets/c372a32f-6dc1-48e8-8ae5-a2a2e31c6465" />

# Part 4 - Accessible Dropdown Menu

1. Let's simulate a basic HTML menu using unordered lists and a button.

```html
<button id="menuButton"
        aria-haspopup="true"
        aria-expanded="false">
  Menu
</button>

<ul id="menu" hidden>
  <li><a href="#">Profile</a></li>
  <li><a href="#">Settings</a></li>
  <li><a href="#">Logout</a></li>
</ul>
```

2. Add the following JavaScript code to interact with the menu when clicking the button:

```javascript
const menuBtn = document.getElementById("menuButton");
const menu = document.getElementById("menu");

menuBtn.addEventListener("click", () => {
  const expanded = menuBtn.getAttribute("aria-expanded") === "true";
  menuBtn.setAttribute("aria-expanded", !expanded);
  menu.hidden = expanded;
});

document.addEventListener("click", (e) => {
  if (!menu.contains(e.target) && e.target !== menuBtn) {
    menu.hidden = true;
    menuBtn.setAttribute("aria-expanded", "false");
  }
});
```

3. Test your implementation. You will observe the following:

- The button toggles the menu
- `aria-expanded` is updated accordingly
- Clicking outside closes menu

Task: How to close the menu using the `Escape` key?

<img width="535" height="640" alt="image" src="https://github.com/user-attachments/assets/e2f9cef8-f163-4d84-8563-a29d58d5136d" />


# Part 5 - Accessibility Tree and Lighthouse accessibility audit

1. Open the Accessibility Tree in DevTools 

<img width="803" height="303" alt="image" src="https://github.com/user-attachments/assets/277ca9a2-a294-4869-8ade-b4f29a310487" />

2. Click on several items in the page and notice the changes in the Accessibility Tree:

<img width="1568" height="753" alt="image" src="https://github.com/user-attachments/assets/49427406-21e6-4e94-bd76-234d50b7005e" />

3. Run a Lighthouse accessibility audit. You might need to add the tool first:

<img width="976" height="836" alt="image" src="https://github.com/user-attachments/assets/b061a448-9e11-49fd-94ff-e4493160f2ed" />

<img width="976" height="566" alt="image" src="https://github.com/user-attachments/assets/2da1477d-4d25-44bd-aab8-8a80b366922a" />

You can only audit webpages using the HTTP/HTTPS protocol. You can use Live Server or Live Preview extensions from Visual Studio Code to have a local server host your web files.

<img width="976" height="927" alt="image" src="https://github.com/user-attachments/assets/f110a8af-f2aa-4dee-a9a7-be511c970105" />
 

## Conclusion

Here's what you learned today:

- Build accessible UI components using **native HTML first**
- Apply **ARIA only when necessary**
- Implement full **keyboard navigation**
- Manage **focus correctly**
- Implement **focus trapping**
- Preserve accessibility in dynamic content
- Inspect the Accessibility Tree in DevTools
