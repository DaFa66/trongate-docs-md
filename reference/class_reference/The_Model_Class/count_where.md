# count_where()


public function count_where(string $column, $value, string $operator = '=', ?string $target_tbl = null): int

## Description

Counts the number of rows in a database table based on custom conditions. This method constructs and executes an SQL query to count the rows in the specified table that match the provided conditions.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| column | string | The name of the table column referred to when fetching results. | N/A | Yes |
| value | mixed | The value that should be matched against the target table column. | N/A | Yes |
| operator | string | (optional) The comparison operator. Default is '='. | = | No |
| target_tbl | string\|null | (optional) The name of the database table to be queried. If not explicitly passed, the table name is assumed to be the value of the first URL segment. | 'First URL segment' | No |

## Return Value


| Type | Description |
| ---|---|
| int | The number of rows matching the conditions. |

## Exceptions


| Exception Type | Description |
| ---|---|
| InvalidArgumentException | Thrown if an invalid operator is provided. |
| RuntimeException | Thrown if the query execution fails. |

## Example Usage

```php
$column = 'status';
$value = 'active';
$operator = '=';
$target_tbl = 'users';

$num_active_users = $this->model->count_where($column, $value, $operator, $target_tbl);
```
