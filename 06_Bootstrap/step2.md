# Step 2: Creating Step Navigation with Bootstrap Tabs

## Bootstrap Tabs Component

Tabs allow users to switch between different content panels.

Important classes:

| Class | Purpose |
| --- | --- |
| `nav` | Navigation container |
| `nav-tabs` | Tab-style navigation |
| `nav-item` | Tab container |
| `nav-link` | Clickable tab |
| `tab-content` | Content wrapper |
| `tab-pane` | Individual panel |

Important attributes:

| Attribute | Purpose |
| --- | --- |
| `data-bs-toggle="tab"` | Activates tab behavior |
| `data-bs-target` | Links tab to content |

## Reference

- [Bootstrap Tabs](https://getbootstrap.com/docs/5.3/components/navs-tabs/)

## Task 2.1: Add wizard steps using Bootstrap Tabs

The wizard will use Bootstrap Tabs to represent each step.

Add the following code inside the `wizard` div.

```html
<ul class="nav nav-tabs mb-4" id="wizardTabs">
	<li class="nav-item">
		<button class="nav-link active" data-bs-toggle="tab" data-bs-target="#step1">
			Step 1
		</button>
	</li>

  <!-- implement the code for a Step 2 element -->

  <!-- implement the code for a Step 3 element -->
</ul>

<div class="tab-content">
	<div class="tab-pane fade show active" id="step1">
		Step 1 content
	</div>

	<div class="tab-pane fade" id="step2">
		Step 2 content
	</div>

	<!-- implement the code for a Step 3 content element -->
</div>
```

## Task 2.2 Complete above code for step 2 (navigation and content) and step 3 (content)

Here is the expected output:

![](./images/step2.png)

[< Back to Step 1](step1.md) | Step 2 | [Go to Step 3 >](step3.md)
