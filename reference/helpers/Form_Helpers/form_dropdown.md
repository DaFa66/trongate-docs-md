# form_dropdown()


function form_dropdown(string $name, array $options, ?string $selected_key = null, ?array $attributes = null): string

## Description

Generates an HTML select menu based on the provided options and parameters.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $name | string | The name attribute for the select element. |
| $options | array | An associative array of options (value => text). |
| $selected_key | string\|null | (Optional) The key of the selected option, if any. Default is `null`. |
| $attributes | array\|null | (Optional) An array of additional HTML attributes for the select element. Default is `null`. |

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML string for the select menu. |

## Example #1


Basic usage of `form_dropdown` with minimal parameters:

```
$name = 'fruits';
$options = ['apple' => 'Apple', 'banana' => 'Banana', 'cherry' => 'Cherry'];
echo form_dropdown($name, $options);
// Output:
// <select name="fruits">
//     <option value="apple">Apple</option>
//     <option value="banana">Banana</option>
//     <option value="cherry">Cherry</option>
// </select>
```

## Example #2


Using `form_dropdown` with a pre-selected value and additional attributes:

```
$name = 'fruits';
$options = ['apple' => 'Apple', 'banana' => 'Banana', 'cherry' => 'Cherry'];
$selected_key = 'banana';
$attributes = [
    'class' => 'dropdown',
    'id' => 'fruit-selector',
    'data-live-search' => 'true',
    'aria-label' => 'Fruit Selection'
];
echo form_dropdown($name, $options, $selected_key, $attributes);
// Output:
// <select name="fruits" class="dropdown" id="fruit-selector" data-live-search="true" aria-label="Fruit Selection">
//     <option value="apple">Apple</option>
//     <option value="banana" selected="selected">Banana</option>
//     <option value="cherry">Cherry</option>
// </select>
```

## Example #3


Adding an initial "placeholder" option and handling edge cases:

```
$name = 'fruits';
$options = ['' => 'Please select...', 'apple' => 'Apple', 'banana' => 'Banana'];
$selected_key = '';
$attributes = ['required' => 'required', 'aria-required' => 'true'];
echo form_dropdown($name, $options, $selected_key, $attributes);
// Output:
// <select name="fruits" required="required" aria-required="true">
//     <option value="" selected="selected">Please select...</option>
//     <option value="apple">Apple</option>
//     <option value="banana">Banana</option>
// </select>
```

## Notes


- All option values and text are HTML-escaped to prevent XSS attacks.
- The `$selected_key` parameter ensures that the corresponding option is marked as selected, if applicable.
- Use the `$attributes` parameter to add any valid HTML attributes to the select element, including data attributes, ARIA attributes, and event handlers.
- The `$attributes` array can include both standard HTML attributes (like `class`, `id`) and custom data attributes (like `data-*`).
