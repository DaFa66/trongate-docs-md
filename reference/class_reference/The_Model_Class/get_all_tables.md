# get_all_tables()


public function get_all_tables(): array

## Description

Retrieves all table names from the database.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not take any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| array | Returns an array of table names. |

## Example Usage

```php
// Retrieve all table names from the database
$tables = $this->model->get_all_tables();

// Display the table names
json($tables);
```
