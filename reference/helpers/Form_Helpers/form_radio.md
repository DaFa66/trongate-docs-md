# form_radio()


function form_radio(string $name, mixed $value = null, mixed $checked = false, ?array $attributes = null): string

## Description

Generates a radio button form field element.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $name | string | The name attribute for the input element. |
| $value | mixed | (optional) The value attribute for the input element. Default is null. |
| $checked | mixed | (optional) Whether the radio button should be checked. Can be boolean, string, or any truthy/falsy value. Default is false. |
| $attributes | array\|null | (optional) Additional attributes for the input element as an associative array. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML input element. |

## Example #1


The code sample below demonstrates the basic usage of the `form_radio` function with default parameters.

```
$name = 'user_option';
$value = 'option1';
$checked = true;
echo form_radio($name, $value, $checked);
// Output: '<input type="radio" name="user_option" value="option1" checked>'
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_radio` function with additional attributes.

```
$name = 'user_option';
$value = 'option2';
$checked = false;
$attributes = ['class' => 'form-control', 'id' => 'option2-input', 'data-custom' => 'custom-data'];
echo form_radio($name, $value, $checked, $attributes);
// Output: '<input type="radio" name="user_option" value="option2" class="form-control" id="option2-input" data-custom="custom-data">'
```
