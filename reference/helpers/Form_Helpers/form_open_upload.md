# form_open_upload()


function form_open_upload(string $location, ?array $attributes = null): string

## Description

Generates the opening tag for an HTML form with file upload support.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $location | string | The URL to which the form will be submitted. |
| $attributes | array\|null | (optional) An array of HTML attributes for the form. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| string | The HTML opening tag for the form with enctype set to "multipart/form-data." |

## Example #1


The code sample below demonstrates the basic usage of the `form_open_upload` function.

```
$location = 'upload.php';
  echo form_open_upload($location);
  // Output:
  // <form action="upload.php" method="post" enctype="multipart/form-data">
```

## Example #2


The code sample below demonstrates a more complex usage of the `form_open_upload` function with additional attributes.

```
$location = 'upload.php';
  $attributes = [
      'id' => 'upload-form',
      'class' => 'form-horizontal',
      'onsubmit' => 'return validateForm()'
  ];
  echo form_open_upload($location, $attributes);
  // Output:
  // <form action="upload.php" method="post" enctype="multipart/form-data" id="upload-form" class="form-horizontal" onsubmit="return validateForm()">
```

## Notes


- This function automatically sets the `enctype` attribute to "multipart/form-data", which is required for file uploads.
- The function internally calls the `form_open()` function to generate the HTML.
- If the `$attributes` array includes an 'enctype' key, it will be overwritten with "multipart/form-data".
- The `method` attribute is set to "post" by default (handled by the `form_open()` function).
- Remember to close your form with the `</form>` tag or use a corresponding `form_close()` function if available.
