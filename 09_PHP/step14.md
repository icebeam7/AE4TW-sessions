## Step 14. Add a script for deleting an employee

In a separate PHP script, you will handle the deletion of an employee record from the database, which will be executed through a form that is submitted via the POST method.

This is the code for process_delete.php script:

```php
<?php
    include 'db_connection.php';

    if ($_SERVER['REQUEST_METHOD'] === 'POST') {
        if (isset($_POST['id']) && is_numeric($_POST['id'])) {
            $id = intval($_POST['id']);

            try {
                $query = "DELETE FROM Employee WHERE Id = :id";
                $stmt = $pdo->prepare($query);
                $stmt->bindParam(':id', $id, PDO::PARAM_INT);

                if ($stmt->execute()) {
                    header('Location: list.php');
                    exit;
                } else {
                    header('Location: delete.php?id=' . $id);
                    exit;
                }
            } catch (PDOException $e) {
                die("Error: " . $e->getMessage());
            }
        } else {
            header('Location: list.php');
            exit;
        }
    } else {
        header('Location: list.php');
        exit;
    }
?>
```

*	First, the db_connection.php script is included to establish a connection to the database using the $pdo object. It then checks if the request method is POST, confirming that the script is being accessed through a form submission. This is a common security measure to prevent unintended actions.

*	Inside the try block, a SQL DELETE query is prepared to remove the employee record with the specified id from the Employee table. The query uses a named placeholder :id to securely bind the id value. The prepare method creates a prepared statement, and the bindParam method binds the id value to the :id placeholder, specifying its type as an integer (PDO::PARAM_INT).

*	The execute method runs the query. If the deletion is successful, the script redirects the user to the employee list page. If the deletion fails for any reason, the user is redirected back to the delete employee page with the id appended as a query parameter, allowing them to retry or view additional details.

*	If an exception occurs during the database operation, the catch block handles the PDOException and terminates the script with an error message. 

*	If the id parameter is invalid or missing, or if the script is accessed without a POST request, the user is redirected to the employee list page as a fallback. This prevents unauthorized or unintended access to the script.

[< Previous Step](step13.md) | Step 14 | [Next step >](step15.md)
