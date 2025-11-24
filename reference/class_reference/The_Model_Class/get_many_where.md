# get_many_where()


public function get_many_where(string $column, $value, ?string $target_table = null): array

## Description

Retrieves multiple records from a database table based on custom conditions. This method constructs and executes an SQL query to retrieve rows where the specified column matches the provided value from the specified table. It returns an array of objects representing the fetched rows. If no records are found, an empty array is returned.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| column | string | The name of the table column referred to when fetching results. | N/A | Yes |
| value | mixed | The value that should be matched against the target table column. | N/A | Yes |
| target_table | string\|null | The name of the database table to be queried. Default is derived from the first URL segment. | 'First URL segment' | No |

## Return Value


| Type | Description |
| ---|---|
| array | An array of objects representing the fetched rows. If no records are found, an empty array is returned. |

## Exceptions


| Exception Type | Description |
| ---|---|
| RuntimeException | Thrown if the query execution fails. |

## Example Usage

```php
// Retrieve multiple records where the 'status' column equals 'active'
$active_users = $this->model->get_many_where('status', 'active', 'users');

// Display the fetched records
json($active_users);
```
