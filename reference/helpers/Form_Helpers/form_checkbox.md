# form_checkbox()


function form_checkbox(string $name, mixed $value = '1', mixed $checked = false, ?array $attributes = null): string

## Description

Generates a checkbox form field element.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $name | string | The name attribute for the input element. |
| $value | mixed | (optional) The value attribute for the input element. Default is '1'. |
| $checked | mixed | (optional) Whether the checkbox should be checked. Can be boolean, string, or any truthy/falsy value. Default is false. |
| $attributes | array\|null | (optional) Additional attributes for the input element as an associative array. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML input element. |

## Example #1


The code sample below demonstrates the basic usage of the `form_checkbox` function with default parameters.

```
$name = 'subscribe';
echo form_checkbox($name);
// Output: '<input type="checkbox" name="subscribe" value="1">'
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_checkbox` function with additional attributes.

```
$name = 'subscribe';
$value = 'yes';
$checked = true;
$attributes = [
    'class' => 'checkbox-input', 
    'id' => 'subscribe-checkbox', 
    'disabled' => 'disabled',
    'data-toggle' => 'tooltip',
    'data-placement' => 'top',
    'title' => 'Subscribe to newsletter'
];
echo form_checkbox($name, $value, $checked, $attributes);
// Output: '<input type="checkbox" name="subscribe" value="yes" checked class="checkbox-input" 
//         id="subscribe-checkbox" disabled data-toggle="tooltip" data-placement="top" 
//         title="Subscribe to newsletter">'
```
