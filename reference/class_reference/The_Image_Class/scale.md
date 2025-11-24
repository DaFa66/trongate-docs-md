# scale()


function scale(float $scale): void

## Description

Scales the currently loaded image by a specified percentage, adjusting both the width and height while maintaining the image's aspect ratio. This method calculates the new dimensions based on the percentage provided and resizes the image accordingly using the internal `resize` method.


**How It Works:**


- The method calculates the new width and height by multiplying the current dimensions by the scaling percentage divided by 100.
- It then resizes the image to the new dimensions using the internal `resize` method.


**Note:** Ensure an image is loaded before calling this method. If no image is loaded, or if the scale value is invalid, an exception is thrown.


**Memory Management:** After scaling and saving the image, consider calling `destroy()` to free up memory, especially in scripts that process multiple or large images.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $scale | float | The scaling percentage. A value of 100 maintains the original size, values less than 100 decrease the size, and values greater than 100 increase the size. Must be a positive number. | N/A |

## Exceptions

Throws an **Exception** if:


- No image is loaded.
- The provided scale value is non-positive.
## Return Value


| Type | Description |
| ---|---|
| void | This method does not return a value but resizes the image in-place. |

## Example Usage

```php
// Example 1: Scaling an image to 50% of its original size
try {
    // Load an image
    $this->image->load('path/to/image.jpg');
    
    // Scale the image to 50% of its original size
    $this->image->scale(50);
    
    // Save the scaled image
    $this->image->save('path/to/scaled_image.jpg');
    
    // Free up memory after saving
    $this->image->destroy();
    
    echo "Image scaled successfully to 50% of its original size.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 2: Scaling an image to 150% of its original size
try {
    $this->image->load('path/to/image.jpg');
    
    // Scale the image to 150% of its original size
    $this->image->scale(150);
    
    // Save the scaled image
    $this->image->save('path/to/enlarged_image.jpg');
    
    // Free up memory after saving
    $this->image->destroy();
    
    echo "Image scaled successfully to 150% of its original size.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 3: Batch scaling multiple images
$image_files = ['image1.jpg', 'image2.jpg', 'image3.jpg'];

foreach ($image_files as $file) {
    try {
        // Load an image
        $this->image->load("path/to/$file");
        
        // Scale the image to 75% of its original size
        $this->image->scale(75);
        
        // Save the scaled image
        $this->image->save("path/to/scaled_$file");
        
        // Free up memory after saving
        $this->image->destroy();
        
        echo "Scaled and saved $file successfully.\n";
    } catch (Exception $e) {
        echo "Error processing $file: " . $e->getMessage() . "\n";
    }
}
```
## Best Practices

- **Validate Scale Value:** Ensure the provided scale value is a positive number to avoid exceptions.
- **Use `destroy()` After Scaling:** In scripts that process multiple or large images, call `destroy()` to free up memory after saving the scaled image.
- **Batch Processing:** When scaling multiple images, always call `destroy()` after each image to prevent memory leaks.
- **Check Aspect Ratio:** Since this method maintains the aspect ratio, be mindful of the original image's dimensions to avoid unexpected results when scaling.
