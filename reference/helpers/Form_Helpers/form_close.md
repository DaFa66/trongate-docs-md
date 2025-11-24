# form_close()


function form_close(): string

## Description

Generates hidden CSRF token input field and a closing form tag.
## Parameters


This function does not accept any parameters.

## Return Value


| Type | Description |
| ---|---|
| string | The generated HTML closing tag for the form, including CSRF token. |

## Example


The code sample below demonstrates the basic usage of the `form_close` function.

```
echo form_open('submit_form');
  echo form_input('username');
  echo form_submit('submit', 'Submit');
  echo form_close();
  
  // Output: 
  // '<form action="submit_form" method="post">
  //  <input type="text" name="username">
  //  <input type="submit" name="submit" value="Submit">
  //  <input type="hidden" name="csrf_token" value="...">
  //  </form>'
```

## Additional Notes


The function automatically handles the insertion of a hidden CSRF token field, so developers do not need to manually include it in their forms.  If a CSRF token is not already present in the session, the function generates one using `bin2hex(random_bytes(32))` and stores it in the session under the key `csrf_token`. This ensures that the CSRF token is available for subsequent form submissions and validations.


The function also plays a role in initializing the rendering of inline form validation errors, if required.  For additional information on this topic, please view the documentation for [displaying validation errors](../../form-handling/displaying-validation-errors.html).
