# form_open()


function form_open(string $location, ?array $attributes = null): string

## Description

Generates the opening tag for an HTML form.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $location | string | The URL to which the form will be submitted. |
| $attributes | array\|null | (optional) An array of HTML attributes for the form. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The HTML opening tag for the form. |

## Example #1


The code sample below demonstrates the basic usage of the `form_open` function.

```
$location = 'items/submit';
  echo form_open($location);
  
  // Output: '<form action="https://example.com/items/submit" method="post">'
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_open` function with additional attributes.

```
$location = 'items/submit';
  $attributes = [
      'id' => 'contact-form',
      'class' => 'form-horizontal',
      'method' => 'get'
  ];
  echo form_open($location, $attributes);
  // Output: '<form action="https://example.com/items/submit" method="get" id="contact-form" class="form-horizontal">'
```

## Notes


- The default method for the form is 'post' if not specified in the attributes.
- If the 'method' key is present in the $attributes array, it will be used as the form method and removed from the attributes list.
- The function automatically escapes all attribute names and values to prevent XSS attacks.
- If the $location is not a valid URL and doesn't start with a forward slash, it will be prepended with DOCS_BASE_URL.
- The function generates only the opening tag of the form. Don't forget to close your form with a </form> tag.
