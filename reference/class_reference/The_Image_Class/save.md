# save()


function save(?string $filename = null, int $compression = 100, ?int $permissions = null): void

## Description

Saves the currently loaded image to a file, with optional compression and file permissions settings. This method handles different image formats (JPEG, GIF, PNG, WEBP) and applies the specified compression level for formats that support it (JPEG, WEBP). File permissions can also be set if provided.


**How It Works:**


- If no filename is provided, the method uses the internal filename stored in the class instance (`$file_name`).
- The image is saved in the format corresponding to the loaded image type (e.g., JPEG, PNG, etc.).
- For JPEG and WEBP formats, the compression level can be adjusted to control the trade-off between file size and image quality.
- Optional file permissions can be set to control access to the saved file.
- Transparency is preserved for formats that support it (e.g., PNG and GIF).


**Note:** While the `save()` method writes the image to disk, it does not release the memory allocated for the image resource. To free up memory after saving, it is recommended to call the `destroy()` method, especially in scripts that process multiple images or large images.
## When to Use destroy() After save()

After calling `save()`, it is often advisable to call `destroy()` to explicitly free the memory allocated for the image resource. Here are some scenarios where using `destroy()` is particularly important:


- **Batch Processing:** When processing multiple images in a loop, failing to free memory after each image can lead to excessive memory usage. Explicitly calling `destroy()` ensures efficient memory management.
- **Large Images:** Working with large images can consume significant memory. Releasing memory immediately after saving helps prevent memory exhaustion.
- **Long-Running Scripts:** In scripts that run for extended periods, memory leaks can accumulate if resources are not freed. Using `destroy()` ensures that memory is released as soon as it is no longer needed.
- **Future-Proofing:** Even in simple scripts that process only one image, calling `destroy()` is a good habit. It makes your code more robust and adaptable for future changes.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $filename | string\|null | Optional. The path where the image file will be saved. If not provided, the method uses the internal default filename (`$file_name`) set in the class. | null |
| $compression | int | Optional. Compression level for JPEG and WEBP images, ranging from 0 (worst quality, smallest file) to 100 (best quality, largest file). | 100 |
| $permissions | int\|null | Optional. File permissions to set on the saved file, using the format (e.g., `0644`). If not specified, the system's default permissions are used. | null |

## Exceptions

Throws an **InvalidArgumentException** if:


- An unsupported image type is encountered.
- Required properties (e.g., internal filename) are not set.


Throws a **RuntimeException** if:


- Writing the file fails.
- Setting the specified file permissions is unsuccessful.
## Return Value


| Type | Description |
| ---|---|
| void | This method does not return a value but ensures that the image is saved to the specified file with the requested settings. |

## Example Usage

```php
// Example 1: Saving a Single Image
try {
    // Load an image
    $this->image->load('path/to/image.jpg');
    
    // Perform image operations (e.g., resize)
    $this->image->resize_to_width(800);
    
    // Save the modified image
    $this->image->save('path/to/output.jpg', 85, 0644);
    
    // Free up memory after saving
    $this->image->destroy();
    
    echo "Image saved successfully, and memory has been freed.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 2: Batch Image Processing
$image_files = ['image1.jpg', 'image2.jpg', 'image3.jpg'];

foreach ($image_files as $file) {
    try {
        // Load an image
        $this->image->load("path/to/$file");
        
        // Perform image operations (e.g., resize)
        $this->image->resize_to_width(800);
        
        // Save the modified image
        $this->image->save("path/to/output/$file", 85, 0644);
        
        // Free up memory after saving
        $this->image->destroy();
        
        echo "Processed and saved $file successfully.\n";
    } catch (Exception $e) {
        echo "Error processing $file: " . $e->getMessage() . "\n";
    }
}
// Memory is efficiently managed for each image
```

```php
// Example 3: Optional Use Case Without destroy()
// In short-lived scripts, destroy() may not be strictly necessary
try {
    $this->image->load('path/to/image.jpg');
    $this->image->resize_to_width(800);
    $this->image->save('path/to/output.jpg', 85, 0644);
    
    // No explicit destroy() call
    echo "Image saved successfully. Memory will be cleaned up automatically at script end.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```
## Best Practices

- **Always Call `destroy()` After `save()`:** This ensures immediate cleanup of memory, even if the script terminates shortly afterward.
- **Batch Processing Requires `destroy()`:** When processing multiple images, failing to free memory after each image can lead to memory exhaustion.
- **Future-Proof Your Code:** Even if your script currently handles only one image, explicitly calling `destroy()` makes your code more robust and adaptable for future changes.
- **Validate File Paths:** Ensure the provided file path is writable and valid to avoid runtime errors.
- **Adjust Compression:** Use appropriate compression levels to balance image quality and file size, especially for web-optimized images.
- **Set Permissions Carefully:** Use file permissions to control access to sensitive images, but avoid overly restrictive settings that might break functionality.
