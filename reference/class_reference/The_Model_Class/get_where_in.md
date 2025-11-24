# get_where_in()


public function get_where_in(string $column, array $values, ?string $target_table = null, string $return_type = 'object'): array

## Description

Retrieves records from a database table where the column's value is within a specified array of values. This method allows for filtering records based on multiple values for a given column.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $column | string | The name of the column to filter by. | N/A | Yes |
| $values | array | The array of values to match against the specified column. | N/A | Yes |
| $target_table | string\|null | The name of the database table to be queried. Default is 'First URL segment'. | 'First URL segment' | No |
| $return_type | string | The type of result to return ('object' or 'array'). | object | No |

## Return Value


| Type | Description |
| ---|---|
| array | Returns an array of objects or arrays representing the fetched rows. |

## Example #1


The following code sample demonstrates how to fetch an array of records from a 'members' table where the 'id' values match those within a specified array of integers. In this example, the table name is not explicitly passed as an argument, so the method will derive the table name from the first URL segment.

```
// Assuming the URL is: http://your-domain.com/members/{method_name}
$member_ids = [1, 2, 3, 4];
$members = $this->model->get_where_in('id', $member_ids);
foreach ($members as $member) {
    echo $member->username.'';
}
```
## Example #2


This example demonstrates explicitly passing the table name and specifying the return type for the records. This approach provides more control over the query execution and result format.

```
$column = 'id';
$values = [1, 2, 3, 4];
$target_table = 'items';
$return_type = 'object';

$items = $this->model->get_where_in($column, $values, $target_table, $return_type);
foreach ($items as $item) {
    echo $item->title;
}
```
