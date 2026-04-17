## Step 9. Get the details of a specific employee

Let’s retrieve the details of a specific employee from the database based on a valid id parameter passed via the URL for securely fetching the corresponding employee data. Add the following code in get_employee.php script:

```php
<?php
if (isset($_GET['id']) && is_numeric($_GET['id'])) {
        $id = intval($_GET['id']);

        try {
            $query = "
                SELECT 
                    e.Id, e.Number, e.FirstName, e.LastName, 
                    e.DepartmentId, e.Position, e.Salary, e.HireDate
                FROM Employee e
                WHERE e.Id = :id
            ";
            $stmt = $pdo->prepare($query);
            $stmt->bindParam(':id', $id, PDO::PARAM_INT);
            $stmt->execute();

            $employee = $stmt->fetch(PDO::FETCH_ASSOC);

            if ($employee) {
                $number = $employee['Number'];
                $firstName = $employee['FirstName'];
                $lastName = $employee['LastName'];
                $departmentId = $employee['DepartmentId'];
                $position = $employee['Position'];
                $salary = $employee['Salary'];
                $hireDate = $employee['HireDate'];
            }
        } catch (PDOException $e) {
            echo "<div class='alert alert-danger'>Error fetching employee data: " . $e->getMessage() . "</div>";
        }
    }
?>
```

*	First, the script verifies with an if condition whether the id parameter exists in the URL and whether it is numeric in order to prevent invalid or malicious input. If the condition is met, the intval function converts the id to an integer, ensuring it is safe to use in the database query.

*	Inside the try block, the SQL SELECT query is prepared to fetch the employee's details from the Employee table. The query uses a WHERE clause with a named placeholder :id to filter the results by the employee's unique identifier. 

*	The prepare method of the $pdo object creates a prepared statement, which is a secure way to execute SQL queries. The bindParam method binds the id value to the :id placeholder, specifying its type as an integer with PDO::PARAM_INT.

*	The execute method runs the query, and the fetch method retrieves the result as an associative array with PDO::FETCH_ASSOC. If an employee record is found, its details are extracted and stored in corresponding variables. These variables can then be used for example to pre-fill form fields for editing.

*	If an error occurs during the database operation, the catch block handles the PDOException and displays an error message inside a styled layer, so that the user is informed of the issue without exposing sensitive details about the database.

[< Previous Step](step8.md) | Step 9 | [Next step >](step10.md)
