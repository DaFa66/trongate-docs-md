# form_input()


function form_input(string $name, ?string $value = null, ?array $attributes = null): string

## Description

Generates a text input form field element.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $name | string | The name attribute for the input element. |
| $value | string\|null | (optional) The value attribute for the input element. Default is null. |
| $attributes | array\|null | (optional) Additional attributes for the input element as an associative array. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML input element. |

## Example #1


The code sample below demonstrates the basic usage of the `form_input` function with default parameters.

```
$name = 'username';
$value = 'john_doe';
echo form_input($name, $value);
// Output: '<input type="text" name="username" value="john_doe">'
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_input` function with additional attributes.

```
$name = 'username';
$value = 'john_doe';
$attributes = ['class' => 'form-control', 'id' => 'username-input', 'placeholder' => 'Enter your username'];
echo form_input($name, $value, $attributes);
// Output: '<input type="text" name="username" value="john_doe" class="form-control" id="username-input" placeholder="Enter your username">'
```
