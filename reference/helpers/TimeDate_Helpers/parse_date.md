# parse_date()


function parse_date(string $date_str): \DateTime|false

## Description

Converts a date string into a date object or returns false.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $date_str | string | The date string to parse (format: "mm/dd/yyyy" or "mm-dd-yyyy"). | N/A |

## Return Value


| Type | Description |
| ---|---|
| \DateTime\|false | Returns a \DateTime object representing the parsed date if successful, otherwise returns false if invalid. |

## Example Usage

```
$result = parse_date("12/25/2023");
if ($result !== false) {
    echo $result->format('Y-m-d');
} else {
    echo "Invalid date string.";
}
// Output: 2023-12-25
```
