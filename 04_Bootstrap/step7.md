# Step 7: Form Validation with JavaScript

## Task 7.1: Validate inputs using JS

In the same `wizard.js` script file, add form validation before moving to step 2:

- Create a `validateStep1` function
- Get a reference to the `value` of the `name` input element (from the first tab)
- Get a reference to the `value` of the `email` input element (from the first tab)
- If `name` OR `email` are empty:
	- Call the showAlert function with message `Please fill all fields` and method `danger`.
	- Return `false`
- Otherwise, return `true`

## Task 7.2: Validate before moving to Step 2

In the tab for `Personal Information`, there is a button that takes the user to the next step. Modify its `onclick` call to invoke the form validation method that you just created, and proceed with the next step in case the validation is successful.

## Task 7.3: Test your code

Test the validation:

- Fill in the name and email and check that it is possible to move to Step 2 when clicking on the `Next` button
- Cleat the name and check that now you can't advance to Step 2 using the `Next` button

[< Back to Step 6](step6.md) | Step 7 | [Go to Step 8 >](step8.md)
