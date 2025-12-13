# Image Manipulation


The Trongate [Image class](documentation-ref/list_refs/class_reference/the-image-class) provides a comprehensive suite of methods for efficient and secure image manipulation within your application. This class supports functionalities like loading, resizing, and saving images. It uses PHP's GD library and supports JPEG, GIF, PNG, and WEBP image formats. Access restrictions are in place to prevent unauthorized access to critical directories such as 'config', 'engine', and 'templates', as well as any files directly under the root application level (e.g., '.htaccess').

## Getting Started


To use the Trongate Image class, you need to instantiate the class and then call its methods. Here’s a basic example:

```php
$image = new Image();

try {
    $image_path = APPPATH . 'public/uploads/image.jpg';
    $image->load($image_path);
    $image->resize_to_width(300);
    $resized_image_path = APPPATH . 'public/uploads/resized_image.jpg';
    $image->save($resized_image_path);
    echo "Image resized successfully.";
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```


This example demonstrates how to load an image from a specific directory, resize it, and save the resized image to another directory, all while using Trongate's APPPATH constant for path management.

> [!NOTE]
> **Just To Let You Know...**
>
> In the above example, the `APPPATH` constant is used to return the absolute file path of the application's root directory.  Additional information about this and other helpful features are available [from here](../0120Helpers_Explained/0080other_helpful_features.md).


## Available Methods


Below is a table listing all the available methods in the Trongate Image class, along with a brief description of each method:


| Method | Description |
| ---|---|
| crop() | Crops the image to specified dimensions from a selected position. |
| destroy() | Frees up memory allocated to the image resource. |
| get_header() | Gets the MIME type header for the currently loaded image. |
| get_height() | Retrieves the height of the currently loaded image. |
| get_width() | Retrieves the width of the currently loaded image. |
| output() | Outputs or returns the image content directly. |
| resize_and_crop() | Resizes and crops the image to specified dimensions. |
| resize_to_height() | Resizes the image to a specified height while maintaining the aspect ratio. |
| resize_to_width() | Resizes the image to a specified width while maintaining the aspect ratio. |
| save() | Saves the currently loaded image to a file. |
| scale() | Scales the image by a given percentage. |
| upload() | Handles the upload and processing of an image file. |

