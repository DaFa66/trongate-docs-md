# describe_table()


public function describe_table(string $table, bool $column_names_only = false): array|false

## Description

Retrieves information about the structure of a database table. By default, it returns details of all columns in the specified table. Optionally, it can return only the column names if instructed.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $table | string | The name of the table whose structure is to be described. | N/A | Required |
| $column_names_only | bool | (optional) Whether to return only column names. Default is false. | false | Optional |

## Return Value


| Type | Description |
| ---|---|
| array\|false | Returns an array of column details or an array of column names if $column_names_only is true. Returns false on failure. |

## Exceptions


| Exception Type | Description |
| ---|---|
| PDOException | Thrown if there is an error executing the SQL query. |

## Example Usage

```php
$table_name = 'users'; // Example table name

// Get detailed information about table structure
$table_info = $this->model->describe_table($table_name);

// Display the information
json($table_info);
```
## Alternative Example

```php
$table_name = 'users'; // Example table name

// Get only column names
$column_names = $this->model->describe_table($table_name, true);

// Display the column names
json($column_names);
```
