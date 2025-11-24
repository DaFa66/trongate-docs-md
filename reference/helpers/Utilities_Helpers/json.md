# json()


function json(mixed $data, ?bool $kill_script = null): void

## Description

Outputs the given data as JSON in a prettified format, suitable for debugging and visualization. This function is especially useful during development for inspecting data structures in a readable JSON format directly in the browser. It optionally allows terminating the script immediately after output, which is useful in API development for stopping further processing.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $data | mixed | The data to be encoded into JSON format. The data can be any type that is encodable into JSON, such as arrays or objects. | N/A |
| $kill_script | bool\|null | Optional. Specifies whether to terminate the script after outputting the JSON. If true, the script execution is halted immediately. | null |

## Return Value


| Type | Description |
| ---|---|
| void | Does not return any value; the output is directly written to the output buffer. |

## Example Usage

```
// Given a data array
$data = ["name" => "John Doe", "age" => 30];

// Display the JSON and continue execution
json($data);

// Output with termination after displaying
json($data, true);
```
