# Building a Responsive Landing Page with Modern CSS

Today's objective is to take a basic HTML landing page and transform it into a professional, responsive UI using modern CSS features, such as:

* CSS Variables
* clamp() fluid typography
* Flexbox & Grid
* minmax()
* aspect-ratio
* Mobile-first approach
* Dark mode with prefers-color-scheme
* Microinteractions

---

# Step 1 — Starter HTML

We begin with a clean, semantic HTML page. We will include a `header`, several `section` elements, and a `footer`. This structure matters because good CSS depends on good HTML.

We are separating structure from presentation. The HTML only defines meaning and hierarchy, not appearance at all.

A really important element will be the `viewport` meta tag. Without it, responsive design does not work correctly on mobile devices.

With that in mind, please create a new HTML file with the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Tech Startup</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>

<header class="navbar">
  <div class="container">
    <h1 class="logo">TechStart</h1>
    <nav>
      <ul class="nav-links">
        <li><a href="#">Home</a></li>
        <li><a href="#">Features</a></li>
        <li><a href="#">Pricing</a></li>
      </ul>
    </nav>
  </div>
</header>

<section class="hero">
  <div class="container">
    <h2>Build Smarter Digital Products</h2>
    <p>Modern solutions for growing startups.</p>
    <button class="btn">Get Started</button>
  </div>
</section>

<section class="features container">
  <div class="card">
    <h3>Fast</h3>
    <p>Optimized for performance.</p>
  </div>
  <div class="card">
    <h3>Secure</h3>
    <p>Enterprise-grade security.</p>
  </div>
  <div class="card">
    <h3>Scalable</h3>
    <p>Built to grow with your business.</p>
  </div>
</section>

<footer class="footer">
  <p>© 2026 TechStart</p>
</footer>

</body>
</html>
```

Screenshot:
<img width="503" height="532" alt="Screenshot 2026-02-27 at 14 34 01" src="https://github.com/user-attachments/assets/5debf3a1-1142-41e2-a354-4ea895ba7543" />


---

# Step 2 — Create a Design System with CSS Variables

Instead of hardcoding colors and spacing everywhere, we will define **design tokens** using **CSS variables**.

You can consider a design token like a reusable variable (color, spacing, typography, and animation) that store design decisions as data, acting as a single source of truth between designers and developers.

This does three important things:

1. Makes the design consistent
2. Makes refactoring easy
3. Simulates how professional design systems work

It can be really helpful. For example, if the brand color changes later, we only have to update one line instead of 50.

Another element that will be used here is `clamp()`. Clamp allows **fluid typography** without media queries. It defines:

* A minimum size
* A preferred scaling value
* A maximum size

Fluid typography is a **responsive** typography technique where the text scales automatically with the screen size.  This is part of modern CSS techniques.

Let's create a new file: `styles.css` and follow the steps:

1. First, add below code. 

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: system-ui, sans-serif;
  line-height: 1.6;
}
```

We have defined a standard "reset" that is used to make layout sizing much more predictable.

- `*` is the (Universal Selector). It targets every single HTML element on the page.
- `*::before` and `*::after` target "pseudo-elements" (decorative elements often created in CSS that are not part of the standard HTML)
- `box-sizing: border-box;` changes the way the browser calculates an element's size. Padding and borders are now included within the specified width and height, rather than being added on top of them

Screenshot:
<img width="509" height="630" alt="Screenshot 2026-02-27 at 14 35 00" src="https://github.com/user-attachments/assets/90245960-54f5-4c2c-9c66-79429118c8ff" />


---

2. Let's define CSS Variables: These will be our **design tokens**, so everything will reuse these elements

Add the following CSS code:

```css
:root {
  --color-primary: #4f46e5;
  --color-dark: #111827;
  --color-light: #f9fafb;
  --color-gray: #6b7280;

  --space-sm: 0.5rem;
  --space-md: 1rem;
  --space-lg: 2rem;

  --radius: 12px;
}
```

Variables are inherited, so they cascade naturally through the DOM.

---

3. Fluid Typography with clamp()

Add following code:

```css
h1 {
  font-size: clamp(1.5rem, 3vw, 2.5rem);
}

h2 {
  font-size: clamp(1.3rem, 2.5vw, 2rem);
}
```

Again, clamp helps you with:
* Responsive text without media queries
* Text scales between min and max size

The `clamp(min, val, max)` function accepts three comma-separated expressions as its parameters:

`min`: The minimum value is the smallest (most negative) value. This is the lower bound in the range of allowed values. If the preferred value is less than this value, the minimum value will be used.

`val`: The preferred value is the expression whose value will be used as long as the result is between the minimum and maximum values.

`max`: The maximum value is the largest (most positive) expression value to which the value of the property will be assigned if the preferred value is greater than this upper bound.

Notice the difference between window sizes:

Small size screenshot:
<img width="625" height="677" alt="Screenshot 2026-02-27 at 14 37 18" src="https://github.com/user-attachments/assets/19c26938-e47a-43f4-847f-702090b6bb5f" />


Larger size screenshot:
<img width="865" height="677" alt="Screenshot 2026-02-27 at 14 37 26" src="https://github.com/user-attachments/assets/29a0eb13-eda3-40d9-a050-9ddfe6ced40b" />


---

# Step 3 — Modifying the Layout 

1. Container Utility:
The **container pattern** is extremely common in real projects. It centers content and limits width for readability.
                                                                                                    
Add following code:

```css
.container {
  width: min(1100px, 90%);
  margin-inline: auto;
}
```

Using `width: min(1100px, 90%)` ensures:

* It never exceeds 1100px
* It never gets too tight on small screens

Screenshot:
<img width="865" height="696" alt="Screenshot 2026-02-27 at 14 39 15" src="https://github.com/user-attachments/assets/72ccd665-cbf5-4738-b080-1ad70fb99203" />

---

2. Navbar with Flexbox

Flexbox is ideal for one-dimensional layouts (horizontal or vertical) alignment. 

We use it to distribute space between the logo and navigation links.

Add following code:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            


```css
.navbar {
  background: white;
  padding: var(--space-md) 0;
}

.navbar .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-links {
  display: flex;
  gap: var(--space-md);
  list-style: none;
  padding: 0;
}

.nav-links a {
  text-decoration: none;
  color: var(--color-dark);
}
```

`gap` instead of `margin`: `gap` is cleaner and avoids `margin` collapsing issues.

Screenshot:
<img width="1302" height="696" alt="Screenshot 2026-02-27 at 14 39 58" src="https://github.com/user-attachments/assets/e2f88986-e104-4110-b8e4-053946e0e11b" />


---

3. Hero Section

**Microinteractions** make interfaces feel alive. A small movement + shadow gives depth perception. We will achieve this by implementing button hovering.

Add following code:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            

```css
.hero {
  padding: var(--space-lg) 0;
  text-align: center;
  background: var(--color-light);
}

.btn {
  background: var(--color-primary);
  color: white;
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: var(--radius);
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.1);
}
```

Screenshot:
<img width="1317" height="728" alt="Screenshot 2026-02-27 at 14 40 30" src="https://github.com/user-attachments/assets/eaf4f08b-fcbe-4866-ad0f-a4c6c03a007c" />

Button-hovering:
<img width="477" height="195" alt="Screenshot 2026-02-27 at 14 50 34" src="https://github.com/user-attachments/assets/a8557590-8514-4fd2-b330-c5a00816dd16" />

---

# Step 4 — Advanced Grid for Features

For the features section, we want **automatic column behavior**.

First, we will move from **Flexbox** to **Grid**:

- Flexbox is one-dimensional.
- Grid is two-dimensional.

Then, we will create a fully responsive layout without hardcoding columns.

1. Replace basic stacking with CSS Grid:

```css
.features {
  display: grid;
  gap: var(--space-lg);
  padding: var(--space-lg) 0;
}

@media (min-width: 768px) {
  .features {
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  }
}
```

Explanation:
`repeat(auto-fit, minmax(250px, 1fr))` means:

* Create as many columns as fit.
* Minimum width is 250px.
* Maximum width distributes remaining space evenly.

This removes the need to manually define breakpoints for columns.

The layout becomes **content-driven** instead of **breakpoint-driven**.

Screenshot:
<img width="1317" height="632" alt="Screenshot 2026-02-27 at 14 41 08" src="https://github.com/user-attachments/assets/0a1195b1-ead7-43d1-891f-06489bbb808c" />


---

2. Now, let's create Style Cards

```css
.card {
  padding: var(--space-lg);
  background: white;
  border-radius: var(--radius);
  box-shadow: 0 10px 25px rgba(0,0,0,0.05);
  transition: transform 0.2s ease;
}

.card:hover {
  transform: translateY(-5px);
}
```

Hover transform on cards: **Transforms** are better than changing margins because they do not trigger layout reflow. They are GPU-accelerated and smoother.

Screenshot:
<img width="1317" height="689" alt="Screenshot 2026-02-27 at 14 41 43" src="https://github.com/user-attachments/assets/f9dbfe88-36f5-4ec5-ab21-1e5209cf8e3e" />


---

# Step 5 — Mobile-First Improvements 

The original version of the page prioritizes **mobile-first design**: Instead of writing `max-width` queries to fix desktop layouts, we enhance layouts progressively with `min-width` media queries.

Advantages of this approach:

* It encourages simplicity
* It reduces CSS overrides
* It improves performance

Let's then enhance our page for larger screens.

1. Improve the hero layout:

```css
@media (min-width: 768px) {
  .hero {
    padding: 6rem 0;
  }
}
```

Screenshots:

<img width="480" height="753" alt="Screenshot 2026-02-27 at 14 51 52" src="https://github.com/user-attachments/assets/f074cad4-64fb-42e7-8784-e8a7c9cba5a2" />


---

2. Implement a Sticky Navbar with Sticky positioning

Modern CSS eliminates several JavaScript use cases. Let's implement one of them: **Sticky Positioning**

```css
.navbar {
  position: sticky;
  top: 0;
  background: white;
  z-index: 1000;
}
```

`position: sticky` allows the navbar to remain visible without JavaScript. It works relative to its parent and becomes fixed once it reaches a scroll threshold.

Screenshot:
<img width="482" height="744" alt="Screenshot 2026-02-27 at 14 54 02" src="https://github.com/user-attachments/assets/cf301d2e-d3f2-452e-a770-e34980118998" />


---

# Step 6 — Dark Mode

**Dark mode** support is expected in modern applications.

However, instead of creating a manual toggle, we respect the user’s system preference.

`prefers-color-scheme` detects whether the user has dark mode enabled in their OS.

With that in mind, let's implement dark mode support in our page. Add below code:

```css
@media (prefers-color-scheme: dark) {
  :root {
    --color-dark: #f9fafb;
    --color-light: #1f2937;
  }

  body {
    background: #111827;
    color: var(--color-dark);
  }

  .navbar {
    background: #1f2937;
  }

  .card {
    background: #1f2937;
  }
}
```

Some considerations:

* We have only overriden variables. This is why using CSS variables earlier was powerful.
* We are not rewriting all styles, we are simply changing design tokens.
* And no JS is needed for this real-world UX enhancement.

Screenshot:

<img width="482" height="744" alt="Screenshot 2026-02-27 at 14 54 54" src="https://github.com/user-attachments/assets/efc408a3-79cd-4445-bccf-83ecefd199eb" />


---

# Step 7 — Microinteractions 

Finally, let's implement a few additional features that help our webpage to look more professional.

1. First, let's add a fade-in animation:

```css
.hero {
  animation: fadeIn 0.8s ease forwards;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
```

- Animation should enhance, not distract. In this case, we use a simple `fade` + `translate` animation.
- We animate `opacity` and `transform` instead of `width`, `height`, or `position` properties that cause layout reflow.
- `opacity` and `transform` are performant and smooth properties.
- Duration and easing: Professional UI uses subtle timing instead of exaggerated motion.
- Nowadays, animation communicates hierarchy and improves perceived performance.

---

## Final Thoughts

We started with plain HTML and improved it by adding:

* A design system
* Fluid typography
* Responsive layout without excessive breakpoints
* Modern Grid techniques
* Dark mode
* Microinteractions

# Final Questions

* Why are we using clamp instead of media queries?
* Why did we use minmax instead of fixed columns?
* Why is it important to implement a mobile-first? website?
* What happens if we remove the variables that were defined at the beginning?



