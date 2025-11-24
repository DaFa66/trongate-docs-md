# segment()


function segment(int $num, ?string $var_type = null): mixed

## Description

Get a specific URL segment.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $num | int | The segment number to retrieve. | N/A |
| $var_type | string\|null | Optional. The desired data type of the segment value. Default is null. | null |

## Return Value


| Type | Description |
| ---|---|
| mixed | The value of the specified URL segment. |

## Example Usage

```
echo segment(1);
// Output: example
```
