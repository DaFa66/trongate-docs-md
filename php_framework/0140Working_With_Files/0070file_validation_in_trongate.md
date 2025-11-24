# File Validation in Trongate


Trongate provides a robust validation system for file uploads, ensuring that uploaded files meet specific criteria such as file type, size, and image dimensions. This guide focuses on the validation aspects of file and image uploads, building on the foundational knowledge from the previous section.

## Key Validation Rules for File Uploads


When handling file uploads, Trongate allows you to define validation rules to ensure that uploaded files meet your application's requirements. These rules are applied using the set_rules() method in the Validation class.

### Common Validation Rules


Here are the most commonly used validation rules for file uploads:


- **allowed_types**: Specifies the allowed file extensions (e.g., `jpg`, `png`, `gif`).
- **max_size**: Specifies the maximum file size in kilobytes (e.g., `2000` for 2MB).
- **max_width**: Specifies the maximum width for images (in pixels).
- **max_height**: Specifies the maximum height for images (in pixels).
- **min_width**: Specifies the minimum width for images (in pixels).
- **min_height**: Specifies the minimum height for images (in pixels).
- **square**: Ensures the image is square (width equals height).

### Example Validation Rules


Here’s an example of how to define validation rules for an image upload:

```php
$this->validation->set_rules('picture', 'Product Picture', 'allowed_types[gif,jpg,jpeg,png]|max_size[2000]|max_width[1200]|max_height[1200]');
```


In this example:


- The file must be one of the following types: `gif`, `jpg`, `jpeg`, or `png`.
- The file size must not exceed 2000 KB (2MB).
- The image width and height must not exceed 1200 pixels.

## Security Checks


Trongate includes built-in security checks to ensure that uploaded files do not contain malicious content, such as PHP code or other dangerous patterns. These checks are automatically performed when using the upload_picture() method.

## Handling Validation Errors


If a file fails validation, Trongate will automatically add an error message to the form_submission_errors array. You can display these errors in your view using the validation_errors() helper function.

```php
echo validation_errors();
```

## Summary of Validation Tests


Below is a table summarizing all the available validation tests for file uploads, sorted alphabetically:


| Validation Test | Description |
| ---|---|
| `allowed_types` | Specifies the allowed file extensions (e.g., `gif`, `jpg`, `png`). |
| `max_height` | Specifies the maximum height for images (in pixels). |
| `max_size` | Specifies the maximum file size in kilobytes (e.g., `2000` for 2MB). |
| `max_width` | Specifies the maximum width for images (in pixels). |
| `min_height` | Specifies the minimum height for images (in pixels). |
| `min_width` | Specifies the minimum width for images (in pixels). |
| `square` | Ensures the image is square (width equals height). |

> [!NOTE]
> **Just To Let You Know...**
>
> More information pertaining to Trongate's in-build validation tests is available from the [Validation Rules Reference](documentation/display/php_framework/form-handling/validation-rules-reference).


> [!TIP]
> **Best Practices**
>
> - Always validate file types to prevent unauthorized file uploads.
> - Set appropriate file size limits to prevent server overload.
> - Use image dimension rules to ensure uploaded images meet your application's requirements.


