# form_email()


function form_email(string $name, ?string $value = null, ?array $attributes = null): string

## Description

Generates an email input form field element.
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


The code sample below demonstrates the basic usage of the `form_email` function with default parameters.

```
$name = 'user_email';
  $value = 'example@example.com';
  echo form_email($name, $value);
  // Output: '<input type="email" name="user_email" value="example@example.com">'
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_email` function with additional attributes.

```
$name = 'user_email';
  $value = 'example@example.com';
  $attributes = ['class' => 'email-input', 'id' => 'email-input', 'placeholder' => 'Enter your email'];
  echo form_email($name, $value, $attributes);
  // Output: '<input type="email" name="user_email" value="example@example.com" class="email-input" id="email-input" placeholder="Enter your email">'
```
