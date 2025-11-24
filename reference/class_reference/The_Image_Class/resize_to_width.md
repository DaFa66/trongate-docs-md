# resize_to_width()


function resize_to_width(int $width): void

## Description

Resizes the currently loaded image to a specified width while maintaining the image's aspect ratio. This method calculates the proportional height required to preserve the aspect ratio based on the new width and then calls the internal `resize` method to adjust the image dimensions.


**How It Works:**


- The method calculates the ratio between the target width and the current width of the image.
- It then calculates the new height by multiplying the current height by this ratio.
- Finally, it resizes the image to the new dimensions using the internal `resize` method.


**Note:** Ensure an image is loaded before calling this method. If no image is loaded, or if the provided width is invalid, an exception is thrown.


**Memory Management:** After resizing and saving the image, consider calling `destroy()` to free up memory, especially in scripts that process multiple or large images.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $width | int | The target width to which the image should be resized. Must be a positive integer. | N/A |

## Exceptions

Throws an **Exception** if:


- No image is loaded.
- The provided width is non-positive.
- The current image width is zero (to prevent division by zero).
## Return Value


| Type | Description |
| ---|---|
| void | This method does not return a value but resizes the image in-place. |

## Example Usage

```php
// Example 1: Resizing an image to a specific width while maintaining aspect ratio
try {
    // Load an image
    $this->image->load('path/to/image.jpg');
    
    // Resize the image to a width of 500 pixels
    $this->image->resize_to_width(500);
    
    // Save the resized image
    $this->image->save('path/to/resized_image.jpg');
    
    // Free up memory after saving
    $this->image->destroy();
    
    echo "Image resized successfully to a width of 500 pixels.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 2: Batch resizing multiple images to a specific width
$image_files = ['image1.jpg', 'image2.jpg', 'image3.jpg'];

foreach ($image_files as $file) {
    try {
        // Load an image
        $this->image->load("path/to/$file");
        
        // Resize the image to a width of 800 pixels
        $this->image->resize_to_width(800);
        
        // Save the resized image
        $this->image->save("path/to/resized_$file");
        
        // Free up memory after saving
        $this->image->destroy();
        
        echo "Resized and saved $file successfully.\n";
    } catch (Exception $e) {
        echo "Error processing $file: " . $e->getMessage() . "\n";
    }
}
```

```php
// Example 3: Resizing an image without calling destroy() (for short-lived scripts)
try {
    $this->image->load('path/to/image.jpg');
    $this->image->resize_to_width(300);
    $this->image->save('path/to/resized_image.jpg');
    
    echo "Image resized successfully. Memory will be freed automatically at script end.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```
## Best Practices

- **Validate Dimensions:** Ensure the provided width is a positive integer to avoid exceptions.
- **Use `destroy()` After Resizing:** In scripts that process multiple or large images, call `destroy()` to free up memory after saving the resized image.
- **Batch Processing:** When resizing multiple images, always call `destroy()` after each image to prevent memory leaks.
- **Check Aspect Ratio:** Be mindful of the original image's aspect ratio to avoid unexpected results when resizing.
