# get_last_part()


function get_last_part(string $str, string $delimiter = '-'): string

## Description

Retrieves the last part of a string based on a delimiter.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $str | string | The input string to retrieve the last part from. | N/A |
| $delimiter | string | Optional. The delimiter used to split the string (default: '-'). | - |

## Return Value


| Type | Description |
| ---|---|
| string | The last part of the input string. |

## Example Usage

```
echo get_last_part("example-string-123");
// Output: '123'

echo get_last_part("example string", ' ');
// Output: 'string'
```
