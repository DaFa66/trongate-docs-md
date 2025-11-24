# count()


public function count(?string $target_tbl = null): int

## Description

Counts the number of rows in a database table. This method constructs and executes an SQL query to count the rows in the specified table. It returns the number of rows found in the table.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| target_tbl | string\|null | The name of the database table to count rows from. If not explicitly passed, the table name is assumed to be the value of the first URL segment. | 'First URL segment' | No |

## Return Value


| Type | Description |
| ---|---|
| int | The number of rows in the specified table. |

## Exceptions


| Exception Type | Description |
| ---|---|
| RuntimeException | Thrown if the query execution fails or if the result cannot be fetched. |

## Example Usage

```php
$num_users = $this->model->count('users');
```
