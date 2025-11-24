# get_width()


function get_width(): int

## Description

Returns the width of the currently loaded image in pixels. This method utilizes PHP's GD library function `imagesx()` to retrieve the width of the image resource.


**Note:** An image must be loaded before calling this method. If no image is loaded, the method throws an **Exception** to prevent misuse and ensure valid output.


**Common Use Cases:**


- Calculating the aspect ratio of an image (in combination with `get_height()`).
- Performing resizing or cropping operations based on the image's dimensions.
- Validating image dimensions before processing.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| N/A | N/A | This method does not accept any parameters. | N/A |

## Exceptions

Throws an **Exception** if no image is loaded. This ensures that the method does not fail silently and provides clear feedback for debugging.
## Return Value


| Type | Description |
| ---|---|
| int | The width of the image in pixels, if an image is loaded. |

## Example Usage

```php
// Example 1: Retrieving the width of an image
try {
    // Load an image
    $this->image->load('path/to/image.jpg');
    
    // Get the width of the image
    $width = $this->image->get_width();
    echo "Width of the image: " . $width . " pixels";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 2: Calculating the aspect ratio of an image
try {
    $this->image->load('path/to/image.jpg');
    $width = $this->image->get_width();
    $height = $this->image->get_height();
    
    $aspect_ratio = $width / $height;
    echo "Aspect ratio of the image: " . $aspect_ratio;
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 3: Validating image dimensions before resizing
try {
    $this->image->load('path/to/image.jpg');
    $width = $this->image->get_width();
    
    if ($width > 1200) {
        echo "Image is too wide. Resizing...";
        $this->image->resize_to_width(1200);
    } else {
        echo "Image width is within acceptable limits.";
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```
## Best Practices

- **Always Check for Loaded Images:** Ensure an image is loaded before calling `get_width()` to avoid exceptions.
- **Combine with `get_height()`:** Use `get_width()` in conjunction with `get_height()` for tasks like calculating aspect ratios or performing resizing operations.
- **Validate Dimensions:** Use this method to validate image dimensions before performing operations like resizing or cropping.
