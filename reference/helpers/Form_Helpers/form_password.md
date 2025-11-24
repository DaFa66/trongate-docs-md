# form_password()


function form_password(string $name, ?string $value = null, ?array $attributes = null): string

## Description

Generates a password input form field element.
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


The code sample below demonstrates the basic usage of the `form_password` function with default parameters.

```
$name = 'user_password';
$value = 'securePass123';
echo form_password($name, $value);
// Output: '<input type="password" name="user_password" value="securePass123">'
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_password` function with additional attributes.

```
$name = 'user_password';
$value = 'securePass123';
$attributes = ['class' => 'form-control', 'id' => 'password-input', 'placeholder' => 'Enter your password'];
echo form_password($name, $value, $attributes);
// Output: '<input type="password" name="user_password" value="securePass123" class="form-control" id="password-input" placeholder="Enter your password">'
```
