# form_label()


function form_label(string $label_text, ?array $attributes = null): string

## Description

Generates an HTML label element with optional attributes.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $label_text | string | The text or HTML to display inside the label element. This content is not escaped by default, so ensure proper sanitization if using user-generated content. |
| $attributes | array\|null | (optional) An associative array of HTML attributes for the label element. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML label element with any provided attributes. |

## Example #1


The code sample below demonstrates the basic usage of the `form_label` function with default parameters.

```
$label_text = 'Username';
echo form_label($label_text);
// Output:
// <label>Username</label>
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_label` function with additional attributes.

```
$label_text = 'Username';
$attributes = ['class' => 'form-label', 'for' => 'username'];
echo form_label($label_text, $attributes);
// Output:
// <label class="form-label" for="username">Username</label>
```

## Notes


- The `$label_text` content is not escaped, allowing for more flexibility, such as including HTML. Be cautious when using user-generated content to avoid XSS vulnerabilities.
- The `$attributes` array allows for any valid HTML attributes to be added to the label element.
