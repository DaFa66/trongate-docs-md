# parse_datetime()


function parse_datetime(string $datetime_str): \DateTime|false

## Description

Parses a datetime string into a date object or returns false.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $datetime_str | string | The datetime string to parse (format: "mm/dd/yyyy HH:MM" or "mm-dd-yyyy HH:MM"). | N/A |

## Return Value


| Type | Description |
| ---|---|
| \DateTime\|false | Returns a \DateTime object representing the parsed datetime if successful, otherwise returns false if invalid. |

## Example Usage

```
$result = parse_datetime("12/25/2023 08:30");
if ($result !== false) {
    echo $result->format('Y-m-d H:i:s');
} else {
    echo "Invalid datetime string.";
}
// Output: 2023-12-25 08:30:00
```
