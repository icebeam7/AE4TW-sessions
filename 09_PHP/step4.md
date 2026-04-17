## Step 4. Edit the employee list script

Modify the `list.php` file according to the following instructions:

1.	In the link/button for adding a new employee, change the href value of the <a> element from registration.html to registration.php

```html
    <div class="d-flex justify-content-end mb-3">
        <a href="registration.php" class="btn btn-success">
          <i class="bi bi-plus-circle me-1"></i> Add New Employee
        </a>
    </div>
```

2.	Delete the sample data included in the <tbody> section of the <table> element:

```html
    <div class="card shadow">
        <div class="card-body">
          <div class="table-responsive">
            <table class="table table-striped table-hover table-bordered align-middle">
              <thead class="table-primary">
                <tr>
                  <th>ID</th>
                  <th>Emp #</th>
                  <th>First Name</th>
                  <th>Last Name</th>
                  <th>Department</th>
                  <th>Position</th>
                  <th>Salary</th>
                  <th>Hire Date</th>
                  <th>Actions</th>
                </tr>
              </thead>
              <tbody>

              </tbody>
            </table>
          </div>
        </div>
    </div>
```
 
3.	Now, the <tbody> section is going to include the information from the Employee table in a formatted, structured way with links for performing actions on the specific employee such as editing or deleting it. The following PHP code replaces the content that was deleted, so it will be inside the <tbody> section. 

```php
              <?php
                include 'db_connection.php';

                try {
                    $query = "
                        SELECT 
                            e.Id, e.Number, e.FirstName, e.LastName, 
                            d.Name AS Department, e.Position, e.Salary, e.HireDate
                        FROM Employee e
                        INNER JOIN Department d ON e.DepartmentId = d.Id
                    ";
                    $stmt = $pdo->query($query);

                    while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
                        echo "<tr>";
                        echo "<td>{$row['Id']}</td>";
                        echo "<td>{$row['Number']}</td>";
                        echo "<td>{$row['FirstName']}</td>";
                        echo "<td>{$row['LastName']}</td>";
                        echo "<td>{$row['Department']}</td>";
                        echo "<td>{$row['Position']}</td>";
                        echo "<td>$" . number_format($row['Salary'], 2) . "</td>";
                        echo "<td>{$row['HireDate']}</td>";
                        echo "<td>
                                <a href='view.php?id={$row['Id']}' class='text-primary me-2' title='View'><i class='bi bi-eye-fill'></i></a>
                                <a href='registration.php?id={$row['Id']}' class='text-warning me-2' title='Edit'><i class='bi bi-pencil-fill'></i></a>
                                <a href='delete.php?id={$row['Id']}' class='text-danger' title='Delete'><i class='bi bi-trash-fill'></i></a>
                              </td>";
                        echo "</tr>";
                    }
                } catch (PDOException $e) {
                    echo "<tr><td colspan='9' class='text-danger'>Error fetching data: " . $e->getMessage() . "</td></tr>";
                }
                ?>
```

 
*	The above PHP code retrieves and displays employee data from the database in an HTML table. It begins by including the db_connection.php file, which establishes a connection to the database using the PDO extension. The $pdo object is created in the included file and available for executing database queries.

*	The try block contains the main logic for fetching and displaying data. A SQL query is defined in the $query variable to retrieve the employee details from the Employee table and joins it with the Department table to fetch the department name. The INNER JOIN ensures that only employees with a valid department association are included in the results.

*	The query method from the $pdo object method executes the SQL query, and the result is stored in the $stmt variable, which is a PDO statement object. 

*	The while loop iterates over the rows returned by the query using fetch method from the $stmt object. The PDO::FETCH_ASSOC argument fetches each row as an associative array, where the column names are the keys.

*	Within the loop, each row's data is dynamically inserted into an HTML `<tr>` element, creating a table row for each employee. The echo statements generate `<td>` elements for each column, formatting the salary using the number_format PHP function.

*	Besides, the HTML code created in PHP also generates `<td>` elements links for viewing, editing, and deleting the employee record. These links include the employee's Id as a query parameter, enabling actions to be performed on specific records.

*	If an error occurs during the query execution, the catch block handles the PDOException. It outputs a single table row with an error message.


[< Previous Step](step3.md) | Step 4 | [Next step >](step5.md)
