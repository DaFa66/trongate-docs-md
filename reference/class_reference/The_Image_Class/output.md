# output()


function output(bool $return = false): ?string

## Description

Outputs or returns the image content directly depending on the `$return` parameter. This method is versatile and can be used to either:


- **Output the image directly to the browser:** When `$return` is `false` (default), the image is sent to the browser as binary data. This is useful for dynamically serving images in web applications.
- **Return the image as a string:** When `$return` is `true`, the image data is captured as a string using output buffering. This is useful for embedding images in APIs, storing them in databases, or further processing.


The method supports various image formats (JPEG, GIF, PNG, WebP) based on the internal image type set within the class.


**Note:** Ensure an image is loaded before calling this method. If no image is loaded, the behavior is undefined.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $return | bool | Determines whether to return the image content as a string (`true`) or output it directly to the browser (`false`). | false |

## Exceptions

This method does not throw any exceptions directly. However, it relies on the internal state of the class and the GD library functions (e.g., `imagejpeg()`, `imagepng()`) to handle image output. If no image is loaded or if the image type is unsupported, the behavior is undefined.
## Return Value


| Type | Description |
| ---|---|
| ?string | Returns the image data as a string if `$return` is `true`. Otherwise, outputs the image directly to the browser and returns `null`. |

## Example Usage

```php
// Example 1: Output the image directly to the browser
try {
    // Load an image
    $this->image->load('path/to/image.jpg');
    
    // Set the appropriate Content-Type header
    header("Content-Type: " . $this->image->get_header());
    
    // Output the image directly to the browser
    $this->image->output();
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 2: Capture the image data as a string
try {
    $this->image->load('path/to/image.png');
    
    // Capture the image data as a string
    $image_data = $this->image->output(true);
    
    if ($image_data !== null) {
        // Use the image data (e.g., embed in an API response)
        echo json_encode([
            'status' => 'success',
            'image' => base64_encode($image_data) // Base64-encoded image
        ]);
    }
} catch (Exception $e) {
    echo json_encode([
        'status' => 'error',
        'message' => $e->getMessage()
    ]);
}
```

```php
// Example 3: Output a WebP image directly to the browser
try {
    $this->image->load('path/to/image.webp');
    
    // Set the appropriate Content-Type header
    header("Content-Type: image/webp");
    
    // Output the image directly to the browser
    $this->image->output();
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```
## Best Practices

- **Set Appropriate Headers:** When outputting images directly to the browser, always set the appropriate `Content-Type` header using `get_header()` to ensure the browser interprets the image correctly.
- **Use Base64 Encoding for APIs:** When embedding images in API responses, consider encoding the image data as a base64 string for compatibility with JSON or other text-based formats.
- **Ensure an Image Is Loaded:** Always load an image before calling `output()` to avoid undefined behavior.
- **Free Memory After Use:** If you no longer need the image after calling `output()`, call `destroy()` to free up memory, especially in batch processing or long-running scripts.
