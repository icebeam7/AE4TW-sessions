## Step 7. Edit the employee registration page (Part 1 – Add a new employee)

1.	At the very beginning of the script, add the following code to include the database connection script and initialize variables for the form fields.

```php
<?php
    include 'db_connection.php';

    $id = $number = $firstName = $lastName = $departmentId = $position = $salary = $hireDate = '';
?>
```

2.	Modify the registration.php file. Update the form with two new attributes:
  a.	An action to point to the process_employee.php script.
  b.	A POST method.

```html
<form action="process_employee.php" method="POST">
```

3.	Add a new hidden input field with the name id as the first element of the form. It will not be visible to the user on the webpage but will still be submitted along with the form data. The value attribute dynamically outputs the value of the $id variable, which was set earlier in the script with an empty string.

```html
<input type="hidden" name="id" value="<?php echo $id; ?>">
```

A hidden input is typically used in forms where an existing record is being updated. The form will eventually be used to edit an employee's details, with the id value representing the unique identifier of the employee in the database. By including this hidden field, the server can identify which record to update when the form is submitted. This approach ensures that the id is securely passed along with the form data without exposing it to the user interface.

4.	For each of the input fields, set the value to the corresponding PHP variable and include the required attribute. Here is the code for the elements that need to be updated:

```html
...
<input type="text" class="form-control" id="empNumber" name="empNumber" value="<?php echo $number; ?>" placeholder="EMP12345" required>
...
<input type="text" class="form-control" id="firstName" name="firstName" value="<?php echo $firstName; ?>" placeholder="Enter first name" required>
...
<input type="text" class="form-control" id="lastName" name="lastName" value="<?php echo $lastName; ?>" placeholder="Enter last name" required>
...
<input type="text" class="form-control" id="position" name="position" value="<?php echo $position; ?>" placeholder="Enter position">
...
<input type="number" class="form-control" id="salary" name="salary" value="<?php echo $salary; ?>" placeholder="e.g., 50000" required>
...
<input type="date" class="form-control" id="hireDate" name="hireDate" value="<?php echo $hireDate; ?>" placeholder="YYYY-MM-DD" required>
```

5.	For the department list in the <select> element, remove all the options except the first one.
```html
            <div class="col-sm-12 col-md-6 col-lg-6">
                <label for="department" class="form-label">Department</label>
                <select class="form-select" id="department" name="department">
                  <option selected disabled>Choose...</option> 

                </select>
            </div>
```

6.	Now, include the following code inside the <select> element, below the first option:

```php
                <?php
                    try {
                        $query = "SELECT Id, Name FROM Department";
                        $stmt = $pdo->query($query);

                        while ($department = $stmt->fetch(PDO::FETCH_ASSOC)) {
                            $selected = ($department['Id'] == $departmentId) ? 'selected' : '';
                            echo "<option value='{$department['Id']}' $selected>{$department['Name']}</option>";
                        }
                    } catch (PDOException $e) {
                        echo "<option value=''>Error loading departments</option>";
                    }
                ?>                    
```

*	The above script dynamically populates the dropdown options for the department field by fetching data from the Department table in the database by using a SQL query. 

*	With the query (from $pdo object) and fetch (from $stmt object), a while loop iterates over the data. For each department, an <option> element is created with the value attribute set to the department’s Id and the display text set to the department’s Name. 

*	The selected attribute is conditionally added to the <option> element if the department Id matches the value of the $departmentId variable in order to ensure that the correct department is pre-selected when editing an employee.



[< Previous Step](step6.md) | Step 7 | [Next step >](step8.md)
