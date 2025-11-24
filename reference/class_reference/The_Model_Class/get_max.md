# get_max()


public function get_max(?string $target_table = null): ?int

## Description

Retrieves the maximum 'id' value from the specified database table. This method constructs and executes an SQL query to fetch the maximum 'id' value from the table. It returns the maximum 'id' value as an integer, or 0 if the table is empty, or null if no table is specified.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| target_table | string\|null | (optional) The name of the database table to query. When a table name is not explicitly passed into the method, the table name will be assumed to be the value of the first URL segment. | 'First URL segment' | No |

## Return Value


| Type | Description |
| ---|---|
| int\|null | Returns the maximum 'id' value from the table. Returns 0 if the table is empty or null if no table is specified. |

## Example Usage #1


In the example below, the table name ('products') is being passed into the method as an argument.

```php
$max_id = $this->model->get_max('products');
```
## Example Usage #2


In this alternative example, no table name has been passed into the method. This means that the table name will be assumed to be the value of the first URL segment.

```php
$max_id = $this->model->get_max();
```
