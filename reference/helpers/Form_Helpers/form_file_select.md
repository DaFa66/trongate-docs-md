# form_file_select()


function form_file_select(string $name, ?array $attributes = null): string

## Description

Generates an HTML file input element.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $name | string | The name attribute for the file input. |
| $attributes | array\|null | (optional) An array of HTML attributes for the file input. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML for the file input element. |

## Example #1


The code sample below demonstrates the basic usage of the `form_file_select` function.

```
$name = 'user_file';
  echo form_file_select($name);
  // Output:
  // <input type="file" name="user_file">
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_file_select` function with additional attributes.

```
$name = 'user_file';
  $attributes = [
      'id' => 'user-file-input',
      'class' => 'form-control-file',
      'accept' => '.pdf,.doc,.docx',
      'multiple' => true
  ];
  echo form_file_select($name, $attributes);
  // Output:
  // <input type="file" name="user_file" id="user-file-input" class="form-control-file" accept=".pdf,.doc,.docx" multiple>
```

## Notes


- The function automatically sets the `type` attribute to 'file'.
- This function internally calls the `form_input()` function to generate the HTML.
- Any attributes passed in the `$attributes` array will be added to the input element, allowing for customization of the file input's behavior and appearance.
- The `multiple` attribute can be added to allow selection of multiple files.
- The `accept` attribute can be used to specify which file types are allowed.
