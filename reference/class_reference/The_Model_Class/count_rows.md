# count_rows()


public function count_rows(string $column, $value, ?string $target_table = null): int

## Description

Counts the number of rows in a database table based on a single condition. This method constructs and executes an SQL query to count the rows in the specified table that match the provided condition.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| column | string | The name of the table column referred to when fetching results. | N/A | Yes |
| value | mixed | The value that should be matched against the target table column. | N/A | Yes |
| target_table | string\|null | (optional) The name of the database table to be queried. If not explicitly passed, the table name is assumed to be the value of the first URL segment. | 'First URL segment' | No |

## Return Value


| Type | Description |
| ---|---|
| int | The number of rows matching the condition. |

## Exceptions


| Exception Type | Description |
| ---|---|
| RuntimeException | Thrown if the query execution fails. |

## Example Usage

```php
$column = 'status';
$value = 'active';
$target_table = 'users';
$num_active_users = $this->model->count_rows($column, $value, $target_table);
```
