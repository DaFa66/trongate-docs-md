# parse_time()


function parse_time(string $time_str): \DateTime|false

## Description

Converts a time string into a date object or returns false.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $time_str | string | The time string to parse (format: "HH:MM"). | N/A |

## Return Value


| Type | Description |
| ---|---|
| \DateTime\|false | Returns a \DateTime object representing the parsed time if successful, otherwise returns false if invalid. |

## Example Usage

```
$result = parse_time("14:30");
if ($result !== false) {
    echo $result->format('Y-m-d H:i:s');
} else {
    echo "Invalid time string.";
}
// Output: Current date with the time set to 14:30:00
```
