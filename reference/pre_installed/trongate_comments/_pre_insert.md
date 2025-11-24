# _pre_insert()


function _pre_insert(array $input): array

## Description

Pre-insert hook to be invoked by API manager before inserting a comment.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $input | array | The input data for insertion. | N/A |

## Return Value


| Type | Description |
| ---|---|
| array | Processed input data with additional parameters. |

## Example Usage

```
$input = [
    'token' => 'some_token_string',
    'params' => [
        'user_id' => 123,
        'date_created' => 1621105200,
        'code' => 'abc123'
    ]
];
$processed_input = _pre_insert($input);
var_dump($processed_input);
/* Output:
array(1) {
  ["params"]=>
  array(3) {
    ["user_id"]=>
    int(123)
    ["date_created"]=>
    int(1621242005)
    ["code"]=>
    string(6) "xY8zBh"
  }
}
*/
```
