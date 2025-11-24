# form_submit()


function form_submit(string $name, ?string $value = null, ?array $attributes = null): string

## Description

Generates an HTML submit button element.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $name | string | The name attribute for the button element. |
| $value | string\|null | (optional) The value of the button. If not provided, defaults to "Submit". Default is null. |
| $attributes | array\|null | (optional) An associative array of HTML attributes for the button. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML submit button element. |

## Example #1


The code sample below demonstrates the basic usage of the `form_submit` function with the default value.

```
$name = 'submit_button';
  echo form_submit($name);
  // Output:
  // <button type="submit" name="submit_button">Submit</button>
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_submit` function with additional attributes and a custom value.

```
$name = 'submit_button';
  $value = 'Send Form';
  $attributes = [
      'id' => 'submit-btn',
      'class' => 'btn btn-primary',
      'onclick' => 'return confirmSubmission()'
  ];
  echo form_submit($name, $value, $attributes);
  
  // Output:
  // <button type="submit" name="submit_button" id="submit-btn" class="btn btn-primary" onclick="return confirmSubmission()">Send Form</button>
```

## Notes


- The function automatically sets the `type` attribute to "submit".
- If no `$value` is provided, the function uses "Submit" as the default button text and value.
- The button's text content is not escaped, so ensure proper sanitization if using user-generated content.
- The `$attributes` array can be used to add any valid HTML attributes to the button element.
- This function generates a `<button>` element rather than an `<input type="submit">`, allowing for more flexible content and styling.
