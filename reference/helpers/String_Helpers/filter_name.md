# filter_name()


function filter_name(string $name, array $allowed_chars = []): string

## Description

Filters and sanitizes a name, typically used for usernames.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $name | string | The input name to be filtered and sanitized. |
| $allowed_chars | array | Optional. An array of allowed characters. |

## Return Value


| Type | Description |
| ---|---|
| string | The filtered and sanitized name. |

## Example Usage

```
$input_name = '<script>alert("Hello");</script>';
$allowed_chars = ['-', '_'];
echo filter_name($input_name, $allowed_chars);
// Output: 'alert("Hello");'
```
