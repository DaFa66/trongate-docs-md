# upload()


function upload(array $data): array

## Description

Handles the entire process of uploading and processing an image file. This method performs the following steps:


- Delegates the initial file upload to the `File` class.
- Loads the uploaded image for further processing.
- Resizes the image if its dimensions exceed the specified maximum width or height.
- Generates a thumbnail if requested.


**Note:** After processing the image (e.g., resizing or saving), it is recommended to call the `destroy()` method to free up memory, especially when handling multiple images or large files.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $data | array | Configuration array with settings for file destination, size limits, resizing dimensions, thumbnail creation, and more. See Configuration Properties table below for full details. | N/A |

## Configuration Properties


| Parameter | Type | Description | Example Values | Default | Required |
| ---|---|---|---|---|---|
| destination | string | The directory path where the uploaded file will be saved. | uploads/images/ | N/A | Yes |
| max_width | int | The maximum allowed width for the image. If the image exceeds this width, it will be resized. | 1200 | 450 | No |
| max_height | int | The maximum allowed height for the image. If the image exceeds this height, it will be resized. | 1200 | 450 | No |
| thumbnail_dir | string | The directory path where thumbnails should be saved, if thumbnail generation is enabled. | uploads/thumbnails/ | '' | No |
| thumbnail_max_width | int | The maximum width for thumbnails. | 120 | 0 | No |
| thumbnail_max_height | int | The maximum height for thumbnails. | 120 | 0 | No |
| upload_to_module | bool | Whether to upload the file to a module-specific directory. If true, uses the module's asset directory. | true/false | false | No |
| make_rand_name | bool | Whether to generate a random filename for the uploaded file to avoid name conflicts. | true/false | false | No |
| targetModule | string | The target module for module-specific uploads. Defaults to the value of `segment(1)`. | my_module | segment(1) | No |

## Return Value


| Type | Description |
| ---|---|
| array | An associative array containing details about the uploaded file, including:<br>          <br>- **file_name** (string): The name of the uploaded file.<br>- **file_path** (string): The full path to the uploaded file.<br>- **file_type** (string): The MIME type of the uploaded file.<br>- **file_size** (int): The size of the uploaded file in bytes.<br>- **thumbnail_path** (string, optional): The full path to the generated thumbnail, if applicable. |

## Exceptions

Throws an **Exception** if:


- The file upload fails.
- There are issues during image processing (e.g., invalid directories or unsupported image types).
## Example Usage

```php
// Example 1: Uploading an image with resizing and thumbnail generation
$config = [
    'destination' => 'uploads/images/',
    'max_width' => 1200,
    'max_height' => 1200,
    'thumbnail_dir' => 'uploads/thumbnails/',
    'thumbnail_max_width' => 120,
    'thumbnail_max_height' => 120,
    'upload_to_module' => true,
    'make_rand_name' => true
];

try {
    $file_info = $this->image->upload($config);
    $this->image->destroy(); // Free up memory after processing
    echo 'File uploaded successfully. Details: ';
    print_r($file_info);
} catch (Exception $e) {
    echo 'Upload failed: ' . $e->getMessage();
}
```

```php
// Example 2: Uploading an image without thumbnail generation
$config = [
    'destination' => 'uploads/images/',
    'max_width' => 800,
    'max_height' => 800,
    'upload_to_module' => false,
    'make_rand_name' => false
];

try {
    $file_info = $this->image->upload($config);
    $this->image->destroy(); // Free up memory after processing
    echo 'File uploaded successfully. Details: ';
    print_r($file_info);
} catch (Exception $e) {
    echo 'Upload failed: ' . $e->getMessage();
}
```
## Best Practices

- **Validate Configuration:** Ensure all required configuration keys (e.g., `destination`) are provided and valid.
- **Use `destroy()` After Upload:** In scripts that process multiple or large images, call `destroy()` to free up memory after processing.
- **Batch Processing:** When uploading multiple images, always call `destroy()` after each image to prevent memory leaks.
- **Check File Permissions:** Ensure the destination directories are writable to avoid upload failures.
