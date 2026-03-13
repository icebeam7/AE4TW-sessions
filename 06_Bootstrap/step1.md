# Step 1: Project Setup

## Adding Bootstrap in your app

You have 3 options to add [Bootstrap](https://getbootstrap.com/) in your application:

- Include it via **CDN**: When you only need to include Bootstrap’s compiled CSS or JS, you can use **jsDelivr**.
- Install via **package manager**: Install Bootstrap’s source Sass and JavaScript files via **npm, RubyGems, Composer, or Meteor**.
- Download the **source code**: Download Bootstrap to get the compiled CSS and JavaScript, source code, or include it with your favorite package managers like npm, RubyGems, and more.

## The container class

The `container` class creates a responsive centered layout with horizontal padding.

Useful container variants:

| Class | Description |
| --- | --- |
| `container` | Responsive fixed width |
| `container-fluid` | Full width |
| `container-lg` | Responsive container activated at large breakpoint |

## Reference

- [Bootstrap Containers](https://getbootstrap.com/docs/5.3/layout/containers/)

# Task 1.1: Add Bootstrap support and a container div

1. Create a file called `form-wizard.html` 

1. Add the Bootstrap CSS CDN. 

1. Create a `div` element that uses the `container` Bootstrap class.

1. Add the Bootstrap JS CDN.

1. Add a reference to a `wizard.js` script located in the `js` folder

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Bootstrap Form Wizard</title>

	<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
	<div class="container mt-5">
		<h2 class="mb-4">User Registration Wizard</h2>

		<div id="alert-area"></div>
		<div id="wizard"></div>
	</div>

	<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"></script>

	<script src="js/wizard.js"></script>
</body>
</html>
```

Save your file and open it in the browser:

![](./images/step1.png)


## Task 1.2: Create a base script

Create a `wizard.js` script file in a `js` folder:

```javascript
function nextStep(step) {

}

function previousStep(step) {

}

function submitForm() {

}

function showAlert(message, type) {

}
```

[< Back to Overview](./overview.md) | Step 1 | [Go to Step 2 >](./step2.md)
