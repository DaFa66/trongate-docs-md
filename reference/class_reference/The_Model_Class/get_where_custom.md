# get_where_custom()


public function get_where_custom(string $column, $value, string $operator = '=', string $order_by = 'id', ?string $target_table = null, ?int $limit = null, ?int $offset = null): array

## Description

Retrieves rows from a database table based on custom conditions. This method constructs and executes an SQL query to fetch rows from the specified table, filtering them based on the provided column, value, and comparison operator. Results can be further customized with optional parameters for ordering, limiting, and offsetting.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| column | string | The name of the table column referred to when fetching results. | N/A | Yes |
| value | mixed | The value that should be matched against the target table column. | N/A | Yes |
| operator | string | The comparison operator. Default is '='. | = | No |
| order_by | string | The column to order results by. Default is 'id'. | 'id' | No |
| target_table | string\|null | The name of the database table to be queried. Default is derived from the first URL segment. | 'First URL segment' | No |
| limit | int\|null | The maximum number of results to return. Default is null. | null | No |
| offset | int\|null | The number of rows to skip before fetching results. Default is null. | null | No |

## Return Value


| Type | Description |
| ---|---|
| array | An array of objects representing the fetched rows. If no records are found, an empty array is returned. |

## Exceptions


| Exception Type | Description |
| ---|---|
| InvalidArgumentException | Thrown if an invalid operator is provided. |
| RuntimeException | Thrown if the query execution fails. |

## Example Usage #1

The code sample below demonstrates how to retrieve rows from a database table where the column 'paid' equals 1, ordered by the default column 'id'. In this example, the table name would be inferred from the first URL segment.

```php
$invoices = $this->model->get_where_custom('paid', 1);
```
## Example Usage #2

The code sample below demonstrates how to fetch rows from the 'orders' table where the 'status' column equals 'pending', ordered by 'order_date' in descending order, limited to 10 results, with an offset of 5.

```php
$orders = $this->model->get_where_custom('status', 'pending', '=', 'order_date DESC', 'orders', 10, 5);
```
## Example Usage #3

In this alternative example, rows are fetched from the 'customers' table where the 'country' column equals 'USA', ordered by 'last_name' in ascending order. No limit or offset is applied.

```php
$customers = $this->model->get_where_custom('country', 'USA', '=', 'last_name', 'customers');
```
## Example Usage #4

The following example retrieves rows from the 'tasks' table where the 'status' column does not equal 'completed', ordered by the default column 'id'.

```php
$incomplete_tasks = $this->model->get_where_custom('status', 'completed', '!=', 'id', 'tasks');
```
## Example Usage #5

This example fetches rows from the 'products' table where the 'price' column is greater than 100, ordered by the 'name' column.

```php
$expensive_products = $this->model->get_where_custom('price', 100, '>', 'name', 'products');
```
## Example Usage #6

The example below retrieves rows from the 'articles' table where the 'title' column contains the word 'apple' (case-insensitive), ordered by the 'created_at' column.

```php
$apple_articles = $this->model->get_where_custom('title', 'apple', 'LIKE', 'created_at', 'articles');
```
