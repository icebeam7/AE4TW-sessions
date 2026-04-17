## Step 6. Create a registration employee script

The `process_employee.php` script adds a new employee record in the Employee database table or updates an existing one, depending if an ID is provided. 

A form (`registration.php`) submits the employee data that is handled here in a POST request. 

This is the code for the `process_employee.php` script:

```php
<?php
    include 'db_connection.php';

    if ($_SERVER['REQUEST_METHOD'] === 'POST') {
        $id = isset($_POST['id']) ? intval($_POST['id']) : null;
        $number = $_POST['empNumber'];
        $firstName = $_POST['firstName'];
        $lastName = $_POST['lastName'];
        $departmentId = intval($_POST['department']);
        $position = $_POST['position'];
        $salary = floatval($_POST['salary']);
        $hireDate = $_POST['hireDate'];

        try {
            if ($id) {
                $query = "
                    UPDATE Employee
                    SET Number = :number, FirstName = :firstName, LastName = :lastName,
                        DepartmentId = :departmentId, Position = :position, Salary = :salary, HireDate = :hireDate
                    WHERE Id = :id
                ";
                $stmt = $pdo->prepare($query);
                $stmt->bindParam(':id', $id, PDO::PARAM_INT);
            } else {
                $query = "
                    INSERT INTO Employee (Number, FirstName, LastName, DepartmentId, Position, Salary, HireDate)
                    VALUES (:number, :firstName, :lastName, :departmentId, :position, :salary, :hireDate)
                ";
                $stmt = $pdo->prepare($query);
            }

            $stmt->bindParam(':number', $number, PDO::PARAM_STR);
            $stmt->bindParam(':firstName', $firstName, PDO::PARAM_STR);
            $stmt->bindParam(':lastName', $lastName, PDO::PARAM_STR);
            $stmt->bindParam(':departmentId', $departmentId, PDO::PARAM_INT);
            $stmt->bindParam(':position', $position, PDO::PARAM_STR);
            $stmt->bindParam(':salary', $salary, PDO::PARAM_STR);
            $stmt->bindParam(':hireDate', $hireDate, PDO::PARAM_STR);

            $stmt->execute();

            header('Location: list.php');
            exit;
        } catch (PDOException $e) {
            die("Error: " . $e->getMessage());
        }
    } else {
        header('Location: registration.php');
        exit;
    }
?>
```

*	The script begins by including the db_connection.php file to establish a connection to the database using the $pdo object.

*	The script checks if the request method is POST, ensuring that it only processes data submitted via a form. If the script is accessed directly without submitting a form, it redirects the user to the registration.php page. It is important that the script is only executed in the intended context.

*	If POST data was found, the form data is retrieved from the $_POST superglobal array. The keys in the array correspond to the names of the html elements in the form (inputs, for example). 

*	If an id is provided, this indicates that the operation is an update; otherwise, it is treated as an insertion of a new employee.

*	Inside the try block, the script constructs the appropriate SQL query based on whether the operation is an update or an insert:
  *	For updates, an UPDATE query is prepared, which modifies the existing record identified by the id. 
  *	For inserts, an INSERT INTO query is prepared to add a new record. 

*	Both queries use named placeholders (:number, :firstName, etc) to prevent SQL injection and improve readability.

*	The bindParam method is used to bind the form data to the named placeholders in the query. This ensures that the data is securely passed to the database with the correct data types (e.g., PDO::PARAM_INT for integers, PDO::PARAM_STR for strings). 

*	After binding the parameters, the query is executed using the execute method.

*	If the operation is successful, the script redirects the user to the list.php page. 

*	If an error occurs during the database operation, the catch block handles the PDOException and terminates the script with an error message.




[< Previous Step](step5.md) | Step 6 | [Next step >](step7.md)
