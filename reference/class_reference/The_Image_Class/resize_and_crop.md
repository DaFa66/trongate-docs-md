# resize_and_crop()


function resize_and_crop(int $width, int $height): void

## Description

Adjusts the image to precisely match specified dimensions by resizing to maintain the aspect ratio and then cropping the excess. This method ensures that the final image fits the exact dimensions provided, even if that involves cropping parts of the image.


**How It Works:**


- If the target aspect ratio matches the original image's aspect ratio, the image is simply resized to the specified dimensions.
- If the target aspect ratio differs, the image is first resized to the dimension that requires less adjustment (width or height) and then cropped to achieve the desired dimensions.


**Common Use Cases:**


- Creating thumbnails with consistent dimensions.
- Ensuring images fit specific UI components (e.g., profile pictures, banners).
- Preparing images for responsive designs where exact dimensions are required.


**Note:** Ensure an image is loaded before calling this method. If no image is loaded or if the dimensions are invalid, an exception is thrown.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $width | int | The desired width of the final image. Must be a positive integer. | N/A |
| $height | int | The desired height of the final image. Must be a positive integer. | N/A |

## Exceptions

Throws an **Exception** if:


- No image is loaded.
- The provided width or height are non-positive values.
## Return Value


| Type | Description |
| ---|---|
| void | This method does not return a value but modifies the image in-place to the specified dimensions. |

## Example Usage

```php
// Example 1: Resizing and cropping an image to 200x200 pixels
try {
    // Load an image
    $this->image->load('path/to/image.jpg');
    
    // Resize and crop it to 200x200 pixels
    $this->image->resize_and_crop(200, 200);
    
    // Save the modified image
    $this->image->save('path/to/output.jpg');
    
    echo "Image resized and cropped successfully.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 2: Resizing and cropping a landscape image to fit a square aspect ratio
try {
    $this->image->load('path/to/landscape.jpg');
    
    // Resize and crop to 300x300 pixels
    $this->image->resize_and_crop(300, 300);
    
    // Save the modified image
    $this->image->save('path/to/output_square.jpg');
    
    echo "Landscape image resized and cropped to square successfully.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 3: Resizing and cropping a portrait image to fit a banner aspect ratio
try {
    $this->image->load('path/to/portrait.jpg');
    
    // Resize and crop to 800x200 pixels (banner dimensions)
    $this->image->resize_and_crop(800, 200);
    
    // Save the modified image
    $this->image->save('path/to/output_banner.jpg');
    
    echo "Portrait image resized and cropped to banner dimensions successfully.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```
## Best Practices

- **Validate Dimensions:** Ensure the provided width and height are positive integers to avoid exceptions.
- **Check Aspect Ratios:** Be mindful of the original image's aspect ratio to avoid excessive cropping.
- **Use for Thumbnails:** This method is ideal for creating thumbnails or images with consistent dimensions.
- **Free Memory After Use:** If you no longer need the image after resizing and cropping, call `destroy()` to free up memory, especially in batch processing or long-running scripts.
