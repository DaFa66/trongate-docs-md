# truncate_str()


function truncate_str(string $value, int $max_length): string

## Description

Truncates a string to a specified maximum length. If the string's length exceeds the maximum, it is shortened and an ellipsis (...) is appended.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $value | string | The input string to be truncated. | N/A |
| $max_length | int | The maximum length of the truncated string. | N/A |

## Return Value


| Type | Description |
| ---|---|
| string | Returns the truncated string with an ellipsis (...) if the original string's length exceeds the maximum length. |

## Example Usage

```
echo truncate_str("Hello World! This is a Test String.", 11);
// Output: Hello World...
```
