# get_where()


public function get_where(int $id, ?string $target_table = null): object|false

## Description

Fetches a single record by its ID from a database table. This method constructs and executes an SQL query to retrieve the record with the specified ID from the specified table. If no record is found, it returns false.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| id | int | The ID of the record to fetch. | N/A | Yes |
| target_table | string\|null | The name of the database table to be queried. If not explicitly passed, the table name is assumed to be the value of the first URL segment. | 'First URL segment' | No |

## Return Value


| Type | Description |
| ---|---|
| object\|false | An object representing the fetched record, or false if no record is found. |

## Exceptions


| Exception Type | Description |
| ---|---|
| RuntimeException | Thrown if the query execution fails. |

## Example Usage #1


The code sample below demonstrates how to fetch a single record from the 'products' table with the ID '123'.

```php
$product_obj = $this->model->get_where(123, 'products');
```
## Example Usage #2


In this alternative example, no table name has been passed into the method. This means that the table name will be assumed to be the value of the first URL segment.

```php
$user_obj = $this->model->get_where(456);
```
