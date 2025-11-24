# get_one_where()


public function get_one_where(string $column, $value, ?string $target_table = null): object|false

## Description

Fetches a single record based on a column value from a database table. This method constructs and executes an SQL query to retrieve the record where the specified column matches the provided value from the specified table. If no record is found, it returns false.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| column | string | The name of the column to filter by. | N/A | Yes |
| value | mixed | The value to match against the specified column. | N/A | Yes |
| target_table | string\|null | (optional) The name of the database table to be queried. When a table name is not explicitly passed into the method, the table name will be assumed to be the value of the first URL segment. | 'First URL segment' | No |

## Return Value


| Type | Description |
| ---|---|
| object\|false | An object representing the fetched record, or false if no record is found. |

## Exceptions


| Exception Type | Description |
| ---|---|
| RuntimeException | Thrown if the query execution fails. |

## Example Usage #1


The code sample below demonstrates how to fetch a single record from the 'users' table where the 'username' column matches the value 'john_doe'.

```php
$user_obj = $this->model->get_one_where('username', 'john_doe', 'users');
```
## Example Usage #2


In this alternative example, no table name has been passed into the method. This means that the table name will be assumed to be the value of the first URL segment.

```php
$record_obj = $this->model->get_one_where('id', 123);
```
