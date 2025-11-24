# form_button()


function form_button(string $name, ?string $value = null, ?array $attributes = null): string

## Description

Generates an HTML button element.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $name | string | The name attribute for the button element. |
| $value | string\|null | (optional) The value of the button. If not provided, defaults to "Submit". Default is null. |
| $attributes | array\|null | (optional) An associative array of HTML attributes for the button. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML button element. |

## Example #1


The code sample below demonstrates the basic usage of the `form_button` function with default parameters.

```
$name = 'action-btn';
echo form_button($name);
// Output:
// <button type="button" name="action-btn">Submit</button>
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_button` function with a custom value and additional attributes.

```
$name = 'action-btn';
$value = 'Click Me';
$attributes = [
    'class' => 'btn btn-primary', 
    'id' => 'custom-button', 
    'onclick' => 'handleClick()',
    'data-toggle' => 'dropdown'
];
echo form_button($name, $value, $attributes);
// Output:
// <button type="button" name="action-btn" class="btn btn-primary" id="custom-button" onclick="handleClick()" data-toggle="dropdown">Click Me</button>
```

## Notes


- The function automatically sets the `type` attribute to "button".
- If no `$value` is provided, the function uses "Submit" as the default button text.
- The button's text content is not escaped, so ensure proper sanitization if using user-generated content.
- The `$attributes` array can be used to add any valid HTML attributes to the button element.
- For custom data attributes or non-standard HTML attributes, include them in the `$attributes` array (e.g., `['data-toggle' => 'dropdown']`).
