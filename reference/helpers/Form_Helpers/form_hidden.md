# form_hidden()


function form_hidden(string $name, string|int|float|null $value = null, ?array $attributes = null): string

## Description

Generates a hidden input form field element.
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


The code sample below demonstrates the basic usage of the `form_hidden` function with default parameters.

```
$name = 'token';
echo form_hidden($name, 'abc123');
// Output: '<input type="hidden" name="token" value="abc123">'
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_hidden` function with additional attributes.

```
$name = 'token';
$value = 'abc123';
$attributes = ['class' => 'hidden-field', 'id' => 'token-field'];
echo form_hidden($name, $value, $attributes);
// Output: '<input type="hidden" name="token" value="abc123" class="hidden-field" id="token-field">'
```
