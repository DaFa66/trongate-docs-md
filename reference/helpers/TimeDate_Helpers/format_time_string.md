# format_time_str()


function format_time_str(string $stored_time_str): string

## Description

Formats a time string.


Accepts a time string ($stored_time_str) expected in 'HH:ii' format and formats it according to the 'h:i' or 'HH:ii' format based on the provided time.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $stored_time_str | string | The time string to be formatted (expected format: 'HH:ii'). | N/A |

## Return Value


| Type | Description |
| ---|---|
| string | The formatted time string as per the 'h:i' or 'HH:ii' format or the original string if an error occurs. |

## Example Usage

```
echo format_time_str("13:45");
// Output: 01:45
```
