# load()


function load(string $template_file, ?array $data = null): void

## Description

Loads a template file with optional data for use within the template.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $template_file | string | The filename of the template to load. | N/A |
| $data | array\|null | (Optional) The data to be passed to the template as an associative array. | null |

## Return Value


| Type | Description |
| ---|---|
| void | This function does not return a value. |

## Example Usage

```
load("template_file.php", ['variable' => 'value']);
```
