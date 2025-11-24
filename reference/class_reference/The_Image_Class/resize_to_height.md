# resize_to_height()


function resize_to_height(int $height): void

## Description

Resizes the currently loaded image to a specified height while maintaining the image's aspect ratio. This method calculates the proportional width required to preserve the aspect ratio based on the new height and then calls the internal `resize` method to adjust the image dimensions.


**How It Works:**


- The method calculates the ratio between the target height and the current height of the image.
- It then calculates the new width by multiplying the current width by this ratio.
- Finally, it resizes the image to the new dimensions using the internal `resize` method.


**Note:** Ensure an image is loaded before calling this method. If no image is loaded, or if the provided height is invalid, an exception is thrown.


**Memory Management:** After resizing and saving the image, consider calling `destroy()` to free up memory, especially in scripts that process multiple or large images.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $height | int | The target height to which the image should be resized. Must be a positive integer. | N/A |

## Exceptions

Throws an **Exception** if:


- No image is loaded.
- The provided height is non-positive.
- The current image height is zero (to prevent division by zero).
## Return Value


| Type | Description |
| ---|---|
| void | This method does not return a value but resizes the image in-place. |

## Example Usage

```php
// Example 1: Resizing an image to a specific height while maintaining aspect ratio
try {
    // Load an image
    $this->image->load('path/to/image.jpg');
    
    // Resize the image to a height of 300 pixels
    $this->image->resize_to_height(300);
    
    // Save the resized image
    $this->image->save('path/to/resized_image.jpg');
    
    // Free up memory after saving
    $this->image->destroy();
    
    echo "Image resized successfully to a height of 300 pixels.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 2: Batch resizing multiple images to a specific height
$image_files = ['image1.jpg', 'image2.jpg', 'image3.jpg'];

foreach ($image_files as $file) {
    try {
        // Load an image
        $this->image->load("path/to/$file");
        
        // Resize the image to a height of 400 pixels
        $this->image->resize_to_height(400);
        
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
    $this->image->resize_to_height(250);
    $this->image->save('path/to/resized_image.jpg');
    
    echo "Image resized successfully. Memory will be freed automatically at script end.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```
## Best Practices

- **Validate Dimensions:** Ensure the provided height is a positive integer to avoid exceptions.
- **Use `destroy()` After Resizing:** In scripts that process multiple or large images, call `destroy()` to free up memory after saving the resized image.
- **Batch Processing:** When resizing multiple images, always call `destroy()` after each image to prevent memory leaks.
- **Check Aspect Ratio:** Be mindful of the original image's aspect ratio to avoid unexpected results when resizing.
