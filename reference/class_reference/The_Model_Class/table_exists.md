# table_exists()


public function table_exists(string $table_name): bool

## Description

Checks whether a specified table exists in the database.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $table_name | string | The name of the table to check for existence. | N/A | Yes |

## Return Value


| Type | Description |
| ---|---|
| bool | True if the specified table exists in the database, false otherwise. |

## Example Usage

```php
$table_exists = $this->model->table_exists('products');
```
