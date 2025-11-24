# format_datetime_str()


function format_datetime_str(string $stored_datetime_str): string

## Description

Formats a date-time string.


Accepts a date-time string ($stored_datetime_str) expected in 'yyyy-mm-dd HH:ii:ss' format and formats it according to the DEFAULT_DATE_FORMAT constant.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $stored_datetime_str | string | The date-time string to be formatted (expected format: 'yyyy-mm-dd HH:ii:ss'). | N/A |

## Return Value


| Type | Description |
| ---|---|
| string | The formatted date-time string as per the DEFAULT_DATE_FORMAT or the original string if an error occurs. |

## Example Usage

```
echo format_datetime_str("2024-05-06 14:30:00");
// Output: 05/06/2024, 14:30
```
