# create_date_from_array()


function create_date_from_array(array $day_vars): DateTime|false

## Description

Attempts to create a DateTime object from provided date and time components.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $day_vars | array | An array containing 'day', 'month', 'year', 'hours', and 'minutes' components of the date and time. | N/A |

## Return Value


| Type | Description |
| ---|---|
| DateTime\|false | Returns a DateTime object if successful, otherwise returns false. |

## Example Usage

```
$day_vars = [
    'day' => 12,
    'month' => 5,
    'year' => 2024,
    'hours' => 14,
    'minutes' => 30
];
$result = create_date_from_array($day_vars);
if ($result !== false) {
    echo $result->format('Y-m-d H:i:s');
} else {
    echo "Unable to create a valid DateTime object.";
}
// Output: 2024-05-12 14:30:00
```
