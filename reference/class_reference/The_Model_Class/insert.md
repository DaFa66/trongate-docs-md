# insert()


public function insert(array $data, ?string $target_table = null): ?int

## Description

Insert a new record into the database table and return the ID of the newly inserted record. This method takes an associative array containing column names as keys and their corresponding values, along with an optional parameter specifying the name of the database table to insert into. It constructs and executes an SQL query to perform the insertion, returning the ID of the newly inserted record or null if insertion fails.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| data | array | An associative array containing column names as keys and their corresponding values. | N/A | Yes |
| target_table | string\|null | (optional) The name of the database table to insert into. When a table name is not explicitly passed into the method, the table name will be assumed to be the value of the first URL segment. | 'First URL segment' | No |

## Return Value


| Type | Description |
| ---|---|
| int\|null | The ID (int) of the newly inserted record, or null if insertion fails. |

## Example Usage #1


The following code demonstrates how to insert a new record into the 'users' table.

```php
$user_data = [
    'username' => 'john_doe',
    'email' => 'john@example.com',
    'password' => 'hashed_password'
];
$new_user_id = $this->model->insert($user_data, 'users');
```
## Example Usage #2


In this example, we insert a new product record into an unspecified database table. Since no second argument has been passed into the method, the table name will be inferred from the first URL segment.

```php
$product_data = [
    'name' => 'Product X',
    'description' => 'A fantastic product',
    'price' => 99.99
];
$new_product_id = $this->model->insert($product_data);
```
