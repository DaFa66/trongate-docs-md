# update_where()


public function update_where(string $column, $column_value, array $data, ?string $target_table = null): bool

## Description

Updates rows in a database table based on a specific condition. This method takes the column to match for the condition, the value to match for the condition, an associative array containing the data to be updated, and an optional parameter specifying the name of the database table. It constructs and executes an SQL query to perform the update, returning true if the update operation was successful and false otherwise.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| column | string | The column to match for the condition. | N/A | Yes |
| column_value | mixed | The value to match for the condition. | N/A | Yes |
| data | array | An associative array containing the data to be updated. | N/A | Yes |
| target_table | string\|null | (optional) The name of the database table. If not provided, the table name will be inferred from the first URL segment. | 'First URL segment' | No |

## Return Value


| Type | Description |
| ---|---|
| bool | Indicates whether the update operation was successful. |

## Example Usage #1


In this example, the table name is inferred from the first URL segment, and the update is performed based on the condition where the column 'status' equals 'active'.

```php
// Fetch current timestamp
$current_time = date('Y-m-d H:i:s');

// Data to update
$data["status"] = "inactive";
$data["updated_at"] = $current_time;

// Update rows where 'status' column equals 'active'
$update_success = $this->model->update_where("status", "active", $data);

if ($update_success) {
    echo "Rows updated successfully!";
} else {
    echo "Failed to update rows.";
}
```
## Example Usage #2


In this alternative example, the table name 'products' has been passed into the method as an argument. The method attempts to execute SQL that modifies table records by setting the 'status' to 'out of stock' and updating the 'updated_at' timestamp. The update operation would **only** be applied to rows where the 'stock_quantity' equals 10.

```php
// Fetch current timestamp
$current_time = date('Y-m-d H:i:s');

// Data to update
$data["status"] = "out of stock";
$data["updated_at"] = $current_time;

// Update rows in the 'products' table where 'stock_quantity' equals 10
$update_success = $this->model->update_where("stock_quantity", 10, $data, "products");

if ($update_success) {
    echo "Rows updated successfully!";
} else {
    echo "Failed to update rows.";
}
```
> [!WARNING]
> **Warning!**
>
> > [!NOTE]
> > ** Warning!
> 
> 
> > [!NOTE]
> > Exercise caution when using this method, especially in environments with complex data relationships or large datasets. Always ensure proper testing and consider potential data consistency issues.
