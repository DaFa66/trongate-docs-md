# query()


public function query(string $sql, ?string $return_type = null): mixed

## Description

Execute a custom SQL query. This method allows executing custom SQL queries. It takes the SQL query to execute as the first parameter and an optional parameter specifying the type of result to return ('object' or 'array'). It returns the result of the query based on the specified return type.


It's important to ensure that the provided SQL query is properly sanitized to prevent SQL injection attacks.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| sql | string | The SQL query to execute. | N/A | Yes |
| return_type | string\|null | (optional) The type of result to return ('object' or 'array'). Default is null. | null | No |

## Return Value


| Type | Description |
| ---|---|
| mixed | Returns the result of the query based on the specified return type. |

## Throws


| Exception | Description |
| ---|---|
| RuntimeException | If the query execution fails. |
| InvalidArgumentException | If the SQL query is potentially vulnerable to SQL injection. |

## Note

It's important to ensure that the provided SQL query is properly sanitized to prevent SQL injection attacks.
## Example Usage


Below is an example of executing a custom SQL query involving a table join to retrieve information about employees and their corresponding departments:

```php
$sql = "SELECT e.name AS employee_name, e.position, d.name AS department_name
        FROM employees e
        JOIN departments d ON e.department_id = d.id";
        
$rows = $this->model->query($sql, 'object');
```
