# format_date_str()


function format_date_str(string $stored_date_str): string

## Description

Formats a date string.


Accepts a date string ($stored_date_str) expected in 'yyyy-mm-dd' format and formats it according to the DEFAULT_DATE_FORMAT constant.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $stored_date_str | string | The date string to be formatted (expected format: 'yyyy-mm-dd'). | N/A |

## Return Value


| Type | Description |
| ---|---|
| string | The formatted date string as per the DEFAULT_DATE_FORMAT or the original string if an error occurs. |

## Example Usage

```
echo format_date_str("2024-05-06");
// Output: 05/06/2024
```
