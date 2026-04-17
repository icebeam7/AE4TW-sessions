## Step 12. Edit the employee data page 

Now, let’s show the details of a specific employee in the Employee view page. Open the view.php script and do the following tasks:

1.	At the very beginning of the script, include the database connection script and retrieve the employee details by reusing scripts that you previously created. And initialize the variables in between.

```php
<?php
    include 'db_connection.php';

    $id = $number = $firstName = $lastName = $departmentId = $position = $salary = $hireDate = '';

    include 'get_employee.php';
?>
```

2.	In the HTML code, delete the layer that includes the Employee ID:

```html
          <div class="col-sm-12 col-md-6 col-lg-3">
            <strong>Employee ID:</strong> 1
          </div>
```

3.	For the employee number, first name, last name, and position, replace the sample data with the corresponding PHP variable:

```php
...
<strong>Employee Number:</strong> <?php echo $number; ?>
...
<strong>First Name:</strong> <?php echo $firstName; ?>
...
<strong>Last Name:</strong> <?php echo $lastName; ?>
...
<strong>Position:</strong> <?php echo $position; ?>
...
```

4.	For the salary, you will replace the sample data with the value formatted as a number with 2 decimal places.

```php
<strong>Salary:</strong> <?php echo number_format($salary, 2); ?>
```
 
5.	For the hire date, you will replace the sample data with the value formatted as a date with day, month, and year:

```php
<strong>Hire Date:</strong> <?php echo date('d-m-Y', strtotime($hireDate)); ?>
```

6.	Finally, for the department name, replace the sample data with the following script in order to retrieve the name from the department table. You will use the prepare, execute, and fetch methods that you have worked with in previous scripts. 

```php
            <strong>Department:</strong>
            <?php
              try {
                  $query = "SELECT Name FROM Department WHERE Id = ?";
                  $stmt = $pdo->prepare($query);
                  $stmt->execute([$departmentId]);
                  $department = $stmt->fetch(PDO::FETCH_ASSOC);
                  echo $department['Name'];
              } catch (PDOException $e) {
                  echo "Error loading department";
              }
            ?>
```

7.	For Back to List, Edit and Delete hyperlinks, change the extension of the targets from .html to .php. Moreover, replace the sample id with the value of the $id variable In Edit and Delete.

```html
    <div class="d-flex justify-content-between mt-4">
      <a href="list.php" class="btn btn-secondary">
        <i class="bi bi-arrow-left"></i> Back to List
      </a>
      <div>
        <a href="registration.php?id=<?php echo $id; ?>" class="btn btn-warning me-2">
          <i class="bi bi-pencil-fill"></i> Edit
        </a>
        <a href="delete.php?id=<?php echo $id; ?>" class="btn btn-danger">
          <i class="bi bi-trash-fill"></i> Delete
        </a>
      </div>
    </div>
```


[< Previous Step](step11.md) | Step 12 | [Next step >](step13.md)
