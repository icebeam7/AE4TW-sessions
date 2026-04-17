## Step 15. Edit the delete employee page 

In `delete.php`, complete the following tasks:

1.	At the very beginning of the script, include the database connection script and retrieve the employee details by reusing scripts that you previously created. And initialize the variables in between.

```php
<?php
    include 'db_connection.php';

    $id = $firstName = $lastName = $departmentId = $position = '';

    include 'get_employee.php';
?>
```

2.	In the HTML code, delete the layer that includes the Employee ID:

```html
<div class="col-sm-12 col-md-6 col-lg-3"><strong>ID:</strong> 1</div>
```

3.	For the employee name and position, replace the sample data with the corresponding PHP variables:

```php
      <div class="col-sm-12 col-md-6 col-lg-3"><strong>Name:</strong> <?php echo $firstName . ' ' . $lastName ; ?> </div>
      <div class="col-sm-12 col-md-6 col-lg-3"><strong>Position:</strong> <?php echo $position; ?></div>
```

4.	For the department name, you need to write a query based on the employee’s department id:

```php
      <div class="col-sm-12 col-md-6 col-lg-3"><strong>Department:</strong> 
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
      </div>
```

5.	Finally, replace the Back to List link from list.html to list.php. Set the form’s action to the process_delete.php script as well as the value of the hidden input to the $id variable.

```php
    <div class="d-flex justify-content-between">
      <a href="list.php" class="btn btn-secondary">
        <i class="bi bi-arrow-left"></i> Back to List
      </a>
      <form action="process_delete.php" method="POST" class="d-inline">
        <input type="hidden" name="id" value="<?php echo $id; ?>">
        <button type="submit" class="btn btn-danger">
          <i class="bi bi-trash-fill"></i> Confirm Delete
        </button>
      </form>
    </div>
```

[< Previous Step](step14.md) | Step 15 | [Next step >](step16.md)
