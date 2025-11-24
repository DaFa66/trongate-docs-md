# exec()


public function exec(string $sql): void

## Description

Executes a SQL statement. This method is primarily intended for usage by Trongate's Module Import Wizard and should not be used in production environments. It allows executing raw SQL queries directly on the database.


It's important to ensure that the provided SQL query is properly sanitized to prevent SQL injection attacks.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| sql | string | The SQL statement to execute. | N/A | Yes |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return any value. |

## Throws


| Exception | Description |
| ---|---|
| Exception | Thrown if the application environment is not set to 'dev'. |
| PDOException | Thrown if an error occurs during the database operation. |

## Note

This method should only be used for development purposes and may produce undesired consequences if used improperly. It is disabled in production environments.
## Example Usage


Below is an example of executing a SQL statement using the `exec()` method:

```php
$sql = "CREATE TABLE example_table (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(255) NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    )";
    
$this->model->exec($sql);
```
