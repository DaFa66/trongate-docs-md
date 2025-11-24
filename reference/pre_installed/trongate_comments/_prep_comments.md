# _prep_comments()


function _prep_comments(array $output): array

## Description

Prepare comments data with formatted dates and user information. This method is typically called via admin.js.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $output | array | The output data containing comments. | N/A |

## Return Value


| Type | Description |
| ---|---|
| array | Processed output data with formatted comments. |

## Example Usage

```
$output = ['body' => '[{"comment":"This is a comment.","user_id":1,"date_created":1621105200,"target_table":"pages","update_id":1,"code":"abc123"}]'];
$processed_output = _prep_comments($output);
var_dump($processed_output);
/* Output:
array(1) {
  ["body"]=>
  string(134) "[{"comment":"This is a comment.","date_created":"Posted by user123 on Thursday 15th of May 2024 at 10:00:00 AM","user_id":1,"target_table":"pages","update_id":1,"code":"abc123"}]"
}
*/
```
