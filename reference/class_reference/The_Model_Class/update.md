# update()


public function update(int $update_id, array $data, ?string $target_table = null): bool

## Description

This method updates a specific record identified by its ID with new data provided as an associative array. Optionally, you can specify the database table to update; if not provided, the table name will be inferred from the first segment of the URL.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| update_id | int | The ID of the record to update. | N/A | Yes |
| data | array | An associative array containing column names as keys and their corresponding values. | N/A | Yes |
| target_table | string\|null | (optional) The name of the database table to update. If not provided, the table name will be inferred from the first URL segment. | 'First URL segment' | No |

## Return Value


| Type | Description |
| ---|---|
| bool | Returns true if the update was successful, false otherwise. |

## Throws


| Exception | Description |
| ---|---|
| RuntimeException | If the query execution fails. |

## Example 1: Updating a User Record


The code sample below assumes a current URL of the form: example.com/users/update/123.

```php
// Data to update
$data["name"] = "John Doe";
$data["email"] = "john@example.com";

// Update the user record with ID 123 using inferred table name
$update_success = $this->model->update(123, $data);

if ($update_success) {
    echo "User record updated successfully!";
} else {
    echo "Failed to update user record.";
}
```
## Example 2: Updating a Customer Record with Explicit Table Name


The code sample below assumes a current URL of the form: example.com/customers/update/456.

```php
// Fetch record ID from URL
$update_id = segment(3, 'int');

// Data to update
$data["name"] = "Alice Smith";
$data["email"] = "alice@example.com";

// Update the customer record in the 'customers' table
$update_success = $this->model->update($update_id, $data, 'customers');

if ($update_success) {
    echo "Customer record updated successfully!";
} else {
    echo "Failed to update customer record.";
}
```
## Example 3: Updating a Record using Alternative Syntax


The code example below uses alternative PHP syntax to initialize a data array.

```php
// ID of the record to update
$update_id = 123;

// Data to update
$data = [
    'first_name' => 'John',
    'last_name' => 'Doe',
    'email' => 'john.doe@example.com'
];

// Perform the update
$update_success = $this->model->update($update_id, $data, 'members');

if ($update_success) {
    echo "Record updated successfully!";
} else {
    echo "Failed to update record.";
}
```
> [!WARNING]
> > [!NOTE]
> > ** Warning!
> 
> 
> > [!NOTE]
> > Exercise caution when using this method, especially in environments with complex data relationships or large datasets. Always ensure proper testing and consider potential data consistency issues.
