# delete()


public function delete(int $id, ?string $target_tbl = null): bool

## Description

Deletes a record from a database table based on its ID. This method takes the ID of the record to delete and an optional parameter specifying the name of the database table. It constructs and executes an SQL query to delete the record, returning true if the delete operation was successful and false otherwise.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| id | int | The ID of the record to delete. | N/A | Yes |
| target_tbl | string\|null | (optional) The name of the database table to delete from. If not explicitly passed, the table name is assumed to be the value of the first URL segment. | 'First URL segment' | No |

## Return Value


| Type | Description |
| ---|---|
| bool | Indicates whether the delete operation was successful. |

## Example Usage

```php
$id = 123; // Example ID of the record to delete
$target_tbl = 'products'; // Example target table

$is_deleted = $this->model->delete($id, $target_tbl);

if ($is_deleted) {
    echo "Record with ID {$id} was successfully deleted from the {$target_tbl} table.";
} else {
    echo "Failed to delete record with ID {$id} from the {$target_tbl} table.";
}
```
