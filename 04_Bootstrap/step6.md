# Step 6: Navigating Steps with JavaScript

## Bootstrap JavaScript API

Bootstrap components can be controlled via JavaScript.

Example: `new bootstrap.Tab(element)`

Key concepts:

| Feature | Description |
| --- | --- |
| `bootstrap.Tab()` | Programmatic tab control |
| `.show()` | Activate tab |
| Component instances | Allow dynamic interaction |

## Reference

- [Bootstrap JavaScript API](https://getbootstrap.com/docs/5.3/getting-started/javascript/)

## Task 6.1: Use Bootstrap JS API to navigate between tabs

Modify `wizard.js` in order to implement the code for the first two methods:

```javascript
function nextStep(step) {
	let tabTrigger = document.querySelector(
		`button[data-bs-target="#step${step}"]`
	);

	let tab = new bootstrap.Tab(tabTrigger);
	tab.show();
}

function previousStep(step) {
	let tabTrigger = document.querySelector(
		`button[data-bs-target="#step${step}"]`
	);

	let tab = new bootstrap.Tab(tabTrigger);
	tab.show();
}
```

## Task 6.2: Test that navigation works between tabs using `Next` and `Back` buttons

[< Back to Step 5](step5.md) | Step 6 | [Go to Step 7 >](step7.md)
