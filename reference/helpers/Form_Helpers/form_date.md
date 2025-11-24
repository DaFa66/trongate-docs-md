# form_date()


function form_date(string $name, ?string $value = null, ?array $attributes = null): string

## Description

Generates a date input form field element.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $name | string | The name attribute for the input element. |
| $value | string\|null | (optional) The value attribute for the input element. Default is null. |
| $attributes | array\|null | (optional) Additional attributes for the input element as an associative array. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML date input element. |

## Example #1


The code sample below demonstrates the basic usage of the `form_date` function with default parameters.

```
$name = 'dob';
$value = '1990-01-01';
echo form_date($name, $value);
// Output: '<input type="date" name="dob" value="1990-01-01">'
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_date` function with additional attributes.

```
$name = 'dob';
$value = '1990-01-01';
$attributes = ['class' => 'form-control', 'id' => 'dob-input', 'min' => '1900-01-01', 'max' => '2100-12-31'];
echo form_date($name, $value, $attributes);
// Output: '<input type="date" name="dob" value="1990-01-01" class="form-control" id="dob-input" min="1900-01-01" max="2100-12-31">'
```
