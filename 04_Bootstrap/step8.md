# 8. Showing Feedback with Bootstrap Alerts

## Bootstrap Alerts

Alert Structure: Use this class pattern:

`alert alert-warning`

Common Variants:

| Class | Meaning |
| --- | --- |
| `alert-success` | success |
| `alert-warning` | caution |
| `alert-danger` | error |
| `alert-info` | informational |

## Reference

- [Bootstrap Alerts](https://getbootstrap.com/docs/5.3/components/alerts/)

## Task 8.1: Display an Alert using JS

In `wizard.js` script, modify the `showAlert` method in order to display a Bootstrap alert that disappears after 3 seconds:

```javascript
function showAlert(message, type) {
	let area = document.getElementById("alert-area");
	let alert = document.createElement("div");

	alert.className = "alert alert-" + type;
	alert.textContent = message;

	area.appendChild(alert);
	setTimeout(() => alert.remove(), 3000);
}
```

## Task 8.2: Verify the Alert

When the user info is incomplete in step 1, you should see an alert:

![](.images/step8.png)

[< Back to Step 7](step7.md) | Step 8 | [Go to Step 9 >](step9.md)

