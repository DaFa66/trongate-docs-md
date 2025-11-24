# crop()


function crop(int $width, int $height, string $trim = 'center'): void

## Description

Adjusts the image to the specified width and height by cropping it according to the provided `$trim` parameter. 
    This method allows precise control over the section of the image to retain, either centering or aligning the crop to one side, 
    based on the focus area specified. If the desired dimensions exceed the original image dimensions, no cropping occurs.


The `$trim` parameter determines the focus area of the crop:


- **'center'**: Crops the image from the center (default behavior).
- **'right'**: Crops the image from the right side.
- **'left'**: No offset is applied, and the crop starts from the left side.
- **Other values**: Default to `'center'` behavior.


This method is ideal for creating uniform image dimensions without distorting the content.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $width | int | The desired width of the cropped image. Must be a positive integer. | N/A |
| $height | int | The desired height of the cropped image. Must be a positive integer. | N/A |
| $trim | string | Optional. Specifies the focus area of the crop: `'center'`, `'right'`, or `'left'`. Defaults to `'center'`. | center |

## Exceptions

Throws an **InvalidArgumentException** if:


- The provided dimensions are non-positive.
- The dimensions exceed the original image's dimensions.
- No image is loaded.
## Return Value


| Type | Description |
| ---|---|
| void | This method modifies the image in-place and does not return a value. |

## Example Usage

```php
// Example 1: Crop an image to 200x200 pixels, focusing on the center
try {
    // Load an image
    $this->image->load('path/to/image.jpg');
    
    // Crop it to 200x200 pixels
    $this->image->crop(200, 200, 'center');
    
    // Free up memory after cropping
    $this->image->destroy();
    
    echo "Image cropped successfully.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 2: Crop an image to 300x300 pixels, focusing on the right side
try {
    $this->image->load('path/to/image.jpg');
    $this->image->crop(300, 300, 'right');
    $this->image->destroy();
    echo "Image cropped successfully.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```php
// Example 3: Attempt to crop with invalid dimensions
try {
    $this->image->load('path/to/image.jpg');
    $this->image->crop(0, 0); // Invalid dimensions
} catch (InvalidArgumentException $e) {
    echo "Error: " . $e->getMessage();
}
```
## Best Practices

- **Call `destroy()` After Cropping:** To free up memory, especially in scripts that process multiple images or large images.
- **Validate Dimensions:** Ensure the desired dimensions are valid and do not exceed the original image dimensions to avoid exceptions.
- **Use Appropriate `$trim` Values:** Choose `'center'`, `'right'`, or `'left'` based on the desired focus area.
