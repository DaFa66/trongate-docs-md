# view()


protected function view(string $view, array $data = [], ?bool $return_as_str = null): ?string

## Description

Renders a view file with optional data. This method can either display the view on the browser or return the generated contents as a string.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $view | string | The name of the view file to render. | N/A |
| $data | array | Optional. An associative array of data to pass to the view. Default is an empty array. | Empty array |
| $return_as_str | bool\|null | Optional. Whether to return the rendered view as a string. Default is null. If set to true, the view content will be returned as a string; if set to false or null, the view will be displayed on the browser. Default is null, which means the view will be displayed. | null |

## Return Value


| Type | Description |
| ---|---|
| string\|null | If $return_as_str is true, the rendered view as a string; otherwise, null. |

## Example Usage

```php
$view_content = $this->view("my_view", ["name" => "John Doe"], true);
echo $view_content; // Output: HTML content of the rendered view
```
