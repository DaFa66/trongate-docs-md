# filter_str()


function filter_str(string $string, array $allowed_tags = []): string

## Description

Filters and sanitizes a string, removing any disallowed HTML tags while preserving allowed ones.


While similar functionality can be achieved using the **out()** function, **filter_str()** offers control over which HTML tags are allowed or removed.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $string | string | The input string to be filtered and sanitized. |
| $allowed_tags | array | Optional. An array of allowed HTML tags. Default is an empty array. |

## Return Value


| Type | Description |
| ---|---|
| string | The filtered and sanitized string. |

## Example Usage

```
$input_string = '<script>alert("Hello");</script>';
$allowed_tags = ['<p>', '<a>'];
echo filter_str($input_string, $allowed_tags);
// Output: 'alert("Hello");'
```
