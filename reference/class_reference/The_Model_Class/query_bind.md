# query_bind()


public function query_bind(string $sql, array $data, ?string $return_type = null): mixed

## Description

Execute a custom SQL query with parameter binding. This method allows executing custom SQL queries with parameter binding. It takes the SQL query to execute as the first parameter, an associative array of parameters to bind to the query as the second parameter, and an optional parameter specifying the type of result to return ('object' or 'array'). It returns the result of the query based on the specified return type.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| sql | string | The SQL query to execute. | N/A | Yes |
| data | array | An associative array of parameters to bind to the query. | N/A | Yes |
| return_type | string\|null | (optional) The type of result to return ('object' or 'array'). Default is null. | null | No |

## Return Value


| Type | Description |
| ---|---|
| mixed | Returns the result of the query based on the specified return type. |

## Throws


| Exception | Description |
| ---|---|
| RuntimeException | If the query execution fails. |

## Example Usage #1


The code sample below demonstrates how to execute a custom SQL query, using query binding with **named parameters**.

```php
// Build the SQL query (using placeholders).
$sql = "SELECT * FROM users WHERE age > :age AND city = :city";

// Named parameters to bind to the query.
$data = [
    'age' => 30,
    'city' => 'New York'
];

// Execute the query using the named parameters.
$rows = $this->model->query_bind($sql, $data, 'object');
```
## Example Usage #2


The code sample below demonstrates how to execute a custom SQL query, using query binding with **unnamed parameters**.

```php
// Build the SQL query (using placeholders).
$sql = "SELECT * FROM products WHERE category = ? AND price > ?";

// Unnamed parameters to bind to the query.
$data = ['Electronics', 100];

// Execute the query using the unnamed parameters.
$rows = $this->model->query_bind($sql, $data, 'array');
```
