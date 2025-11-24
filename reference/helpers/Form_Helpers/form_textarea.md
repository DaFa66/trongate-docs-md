# form_textarea()


function form_textarea(string $name, ?string $value = null, ?array $attributes = null): string

## Description

Generates an HTML textarea element.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $name | string | The name attribute for the textarea element. |
| $value | string\|null | (optional) The initial value of the textarea. If not provided, it will be empty. |
| $attributes | array\|null | (optional) An associative array of HTML attributes for the textarea. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML textarea element. |

## Example #1


The code sample below demonstrates the basic usage of the `form_textarea` function with default parameters.

```
$name = 'comments';
$value = 'Your feedback here...';
echo form_textarea($name, $value);
// Output: '<textarea name="comments">Your feedback here...</textarea>'
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_textarea` function with additional attributes.

```
$name = 'comments';
$value = 'Your feedback here...';
$attributes = ['class' => 'form-control', 'id' => 'comments-textarea', 'rows' => '5', 'cols' => '50'];
echo form_textarea($name, $value, $attributes);
// Output: '<textarea name="comments" class="form-control" id="comments-textarea" rows="5" cols="50">Your feedback here...</textarea>'
```
