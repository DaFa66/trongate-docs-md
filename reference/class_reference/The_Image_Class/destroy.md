# destroy()


function destroy(): void

## Description

Frees up memory allocated to the image resource stored in this class's instance. This method should be invoked when the image is no longer needed, especially in scripts that process multiple or large images. Properly releasing memory helps prevent memory leaks and ensures efficient management of system resources.


Failure to call this method in scenarios involving multiple or large images can lead to increased memory usage and potential performance degradation.


**When to Use `destroy()`:**


- After modifying the image (e.g., resizing, cropping, saving).
- When the image is no longer needed in the script.
- In batch processing or long-running scripts to prevent memory leaks.


**When `destroy()` Is Not Needed:**


- After read-only operations like `get_header()`, `get_height()`, or `get_width()`. These methods do not modify the image or allocate additional memory, so calling `destroy()` is unnecessary.
- In short-lived scripts (e.g., scripts that terminate immediately after processing an image), calling `destroy()` is optional, as PHP automatically frees memory at the end of script execution. However, it is still considered a best practice to explicitly call `destroy()` for clean and predictable memory management.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| N/A | N/A | This method does not accept any parameters. | N/A |

## Exceptions

This method does not throw any exceptions. It safely checks if an image resource exists before attempting to destroy it. If no image is loaded, the method does nothing.
## Return Value


| Type | Description |
| ---|---|
| void | This method does not return a value but ensures that the memory associated with the image resource is freed. |

## Example Usage

```php
// Example 1: Freeing memory after processing a single image
try {
    // Load an image
    $this->image->load('path/to/image.jpg');
    
    // Perform image operations (e.g., resize, crop, etc.)
    $this->image->resize_to_width(800);
    
    // Save the modified image
    $this->image->save('path/to/output.jpg');
    
    // Free up memory after processing
    $this->image->destroy();
    
    echo "Image processing completed, and memory has been freed.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 2: Batch processing multiple images
$image_files = ['image1.jpg', 'image2.jpg', 'image3.jpg'];

foreach ($image_files as $file) {
    try {
        // Load an image
        $this->image->load("path/to/$file");
        
        // Perform image operations
        $this->image->resize_to_width(800);
        
        // Save the modified image
        $this->image->save("path/to/output/$file");
        
        // Free up memory after processing each image
        $this->image->destroy();
        
        echo "Processed and saved $file successfully.\n";
    } catch (Exception $e) {
        echo "Error processing $file: " . $e->getMessage() . "\n";
    }
}
```

```php
// Example 3: Optional use in short-lived scripts
try {
    $this->image->load('path/to/image.jpg');
    $this->image->resize_to_width(800);
    $this->image->save('path/to/output.jpg');
    
    // No explicit destroy() call (memory will be freed automatically at script end)
    echo "Image processing completed.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```
## Best Practices

- **Always Call `destroy()` in Long-Running Scripts:** In scripts that run for extended periods or process multiple images, explicitly calling `destroy()` ensures efficient memory management and prevents memory leaks.
- **Use in Batch Processing:** When processing multiple images in a loop, call `destroy()` after each image to free memory before loading the next one.
- **Optional in Short-Lived Scripts:** In scripts that terminate immediately after processing an image, calling `destroy()` is optional but still recommended for clean and predictable memory management.
- **No Need for `destroy()` After Read-Only Operations:** Methods like `get_header()`, `get_height()`, and `get_width()` do not modify the image or allocate additional memory, so calling `destroy()` is unnecessary after using them.
