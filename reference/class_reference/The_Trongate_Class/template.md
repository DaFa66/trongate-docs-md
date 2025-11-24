# template()


protected function template(string $template_name, array $data = []): void

## Description

Renders a specific template view by calling a corresponding method in the Templates controller class.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $template_name | string | The name of the template method to be called. | N/A |
| $data | array | Optional. An associative array containing data to be passed to the template method. | [] |

## Return Value


| Type | Description |
| ---|---|
| void | This function does not return a value. |

## Example Usage

```
$template_name = "my_template";
$data = ['variable1' => 'value1', 'variable2' => 'value2'];
template($template_name, $data);
```
