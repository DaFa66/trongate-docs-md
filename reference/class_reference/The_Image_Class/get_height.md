# get_height()


function get_height(): int

## Description

Returns the height of the currently loaded image in pixels. This method utilizes PHP's GD library function `imagesy()` to retrieve the height of the image resource.


**Note:** An image must be loaded before calling this method. If no image is loaded, the method throws an **Exception** to prevent misuse and ensure valid output.


**Common Use Cases:**


- Calculating the aspect ratio of an image (in combination with `get_width()`).
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
| int | The height of the image in pixels, if an image is loaded. |

## Example Usage

```php
// Example 1: Retrieving the height of an image
try {
    // Load an image
    $this->image->load('path/to/image.jpg');
    
    // Get the height of the image
    $height = $this->image->get_height();
    echo "Height of the image: " . $height . " pixels";
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
    $height = $this->image->get_height();
    
    if ($height > 1000) {
        echo "Image is too tall. Resizing...";
        $this->image->resize_to_height(1000);
    } else {
        echo "Image height is within acceptable limits.";
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```
## Best Practices

- **Always Check for Loaded Images:** Ensure an image is loaded before calling `get_height()` to avoid exceptions.
- **Combine with `get_width()`:** Use `get_height()` in conjunction with `get_width()` for tasks like calculating aspect ratios or performing resizing operations.
- **Validate Dimensions:** Use this method to validate image dimensions before performing operations like resizing or cropping.
