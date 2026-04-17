## Step 3. Set the connection to the database

Let’s setup a connection to the MySQL database using the PDO extension (PHP Data Objects). PDO provides a secure and consistent way to interact with different database providers. 

This is the code for the `db_connection.php` script:

```php
<?php
    $host = 'localhost';
    $dbName = 'CompanyDB';
    $username = 'root';
    $password = 12345;

    try {
        $pdo = new PDO("mysql:host=$host;dbname=$dbName;charset=utf8mb4", $username, $password);

        $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        //echo "Connected successfully to the database.";
    } catch (PDOException $e) {
        die("Connection failed: " . $e->getMessage());
    }
?>
```

*	4 variables are defined first to store the database connection details, such as the hostname, the database name, the username, and the password. Replace the username and password with the credentials that you use to connect to MySQL, as they are used for authenticating and connecting to the database in our application.

*	In the try block, we attempt to create a new PDO instance. The PDO constructor is called with a DSN string (Data Source Name), which specifies the database type (mysql), the host, the database name, and the character set (utf8mb4). The $username and $password variables are also passed to authenticate the connection. 

*	If the connection is successful, the script sets an attribute on the PDO object using the setAttribute method, PDO::ATTR_ERRMODE to PDO::ERRMODE_EXCEPTION in order to ensure that any database errors will throw exceptions. This is a best practice as it makes error handling more robust and predictable.

*	If the connection fails for any reason, the catch block is executed. It catches exceptions of type PDOException, which are thrown by the PDO class when an error occurs. The script then terminates execution using the die function and outputs an error message that includes the exception's message ($e->getMessage()) in order to provide useful debugging information about why the connection failed.
 
The above script will be imported (reused) by other PHP files using the `include` statement.

[< Previous Step](step2.md) | Step 3 | [Next step >](step4.md)
