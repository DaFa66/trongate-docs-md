# form_number()


function form_number(string $name, string|int|float|null $value = null, ?array $attributes = null): string

## Description

Generates a number input form field element.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $name | string | The name attribute for the input element. |
| $value | string\|int\|float\|null | (optional) The value attribute for the input element. Default is null. |
| $attributes | array\|null | (optional) Additional attributes for the input element as an associative array. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML input element. |

## Example #1


The code sample below demonstrates the basic usage of the `form_number` function with default parameters.

```
$name = 'quantity';
$value = 10;
echo form_number($name, $value);
// Output: '<input type="number" name="quantity" value="10">'
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_number` function with additional attributes.

```
$name = 'quantity';
$value = 10;
$attributes = ['class' => 'form-control', 'id' => 'quantity-input', 'min' => '1', 'max' => '100'];
echo form_number($name, $value, $attributes);
// Output: '<input type="number" name="quantity" value="10" class="form-control" id="quantity-input" min="1" max="100">'
```
