# get()


public function get(?string $order_by = null, ?string $target_tbl = null, ?int $limit = null, int $offset = 0): array

## Description

Retrieves rows from a database table based on optional parameters. This method constructs and executes an SQL query to fetch rows from the specified table, ordering them as specified, with optional limits and offsets.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| order_by | string\|null | The column to order results by. Default is 'id'. | 'id' | No |
| target_tbl | string\|null | The name of the database table to query. Default is derived from the first URL segment. | 'First URL segment' | No |
| limit | int\|null | The maximum number of results to return. Default is null. | null | No |
| offset | int | The number of rows to skip before fetching results. Default is 0. | 0 | No |

## Return Value


| Type | Description |
| ---|---|
| array | An array of objects representing the fetched rows. |

## Example Usage #1


The code sample below demonstrates how to retrieve all rows from a table.  In this example, the table name is not explicitly passed into the method.  This means that the table name would be assumed to be the value of the first URL segment.

```php
$rows = $this->model->get();
```
## Example Usage #2


The code sample below demonstrates how to retrieve rows from a specific table, ordered by 'id' descending.  In this example, the second argument ('orders') indicates the name of the table to be queried.

```php
$rows = $this->model->get('id desc', 'orders');
```
## Example Usage #3


The code sample below demonstrates how to retrieve rows from a specific table, named 'products'.    The results, in this instance, would be ordered by 'name' and limited to 10 results, with an offset of 5.

```php
$rows = $this->model->get('name', 'products', 10, 5);
```
