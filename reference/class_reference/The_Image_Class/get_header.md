# get_header()


function get_header(): string

## Description

This method returns the MIME type corresponding to the image format of the currently loaded image. The MIME type is essential for setting correct HTTP `Content-Type` headers when serving images directly from PHP scripts or APIs.


If no image is loaded or the image type has not been set, this method throws an **InvalidArgumentException** to prevent misuse and aid in debugging.


**Common Use Cases:**


- Serving images dynamically in web applications.
- Setting the `Content-Type` header for image downloads or API responses.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| N/A | N/A | This method does not accept any parameters. | N/A |

## Exceptions

Throws an **InvalidArgumentException** if:


- No image has been loaded.
- The image type is not set.
## Return Value


| Type | Description |
| ---|---|
| string | Returns the MIME type of the image, suitable for HTTP `Content-Type` headers (e.g., `'image/jpeg'`, `'image/png'`). |

## Example Usage

```php
// Example 1: Serving an image directly to the browser
try {
    // Load an image
    $this->image->load('path/to/image.jpg');
    
    // Get the MIME type
    $mime_type = $this->image->get_header();
    
    // Set the Content-Type header
    header("Content-Type: " . $mime_type);
    
    // Output the image
    echo $this->image->output();
} catch (InvalidArgumentException $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 2: Using get_header() in an API response
try {
    $this->image->load('path/to/image.png');
    $mime_type = $this->image->get_header();
    
    // Return the image as part of an API response
    header("Content-Type: " . $mime_type);
    echo json_encode([
        'status' => 'success',
        'image' => base64_encode($this->image->output(true)) // Output image as base64
    ]);
} catch (InvalidArgumentException $e) {
    header("Content-Type: application/json");
    echo json_encode([
        'status' => 'error',
        'message' => $e->getMessage()
    ]);
}
```
## Best Practices

- **Always Check for Loaded Images:** Ensure an image is loaded before calling `get_header()` to avoid exceptions.
- **Use in Dynamic Image Serving:** This method is particularly useful when serving images dynamically in web applications or APIs.
- **Combine with `output()`:** Use `get_header()` in conjunction with the `output()` method to serve images directly to the browser.
