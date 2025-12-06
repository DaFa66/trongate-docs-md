# upload_picture()


protected function upload_picture(array $config): ?array

## Description

Handles picture uploads within the Trongate framework with optional thumbnail generation. This method processes uploaded images, performs validation, handles resizing, and optionally generates thumbnails based on the provided configuration.


**Core Features:**


- Validates and processes image uploads
- Supports automatic image resizing
- Optional thumbnail generation
- Flexible storage in either module assets or public directory
- Supports filename randomization
## Parameters


| Parameter | Type | Description | Required |
| ---|---|---|---|
| $config | array | Core configuration options:<br><br>- `destination`: Target upload directory path<br>- `max_width`: Maximum width for main image<br>- `max_height`: Maximum height for main image<br>- `upload_to_module`: Whether to store in module assets<br>- `make_rand_name`: Whether to randomize filenames<br><br><br>          Optional thumbnail settings:<br><br>- `thumbnail_dir`: Directory for thumbnails<br>- `thumbnail_max_width`: Maximum thumbnail width<br>- `thumbnail_max_height`: Maximum thumbnail height | Yes |

## Return Value


| Type | Description |
| ---|---|
| array\|null | Returns an array containing:<br><br>- `file_name`: Name of the uploaded file<br>- `file_path`: Full path to the uploaded file<br>- `file_type`: MIME type of the file<br>- `file_size`: File size in bytes<br>- `thumbnail_path`: Path to thumbnail (if generated) |

## Example Usage

```php
// Example 1: Basic image upload without thumbnails
function submit_product_picture($update_id) {
    $this->module('trongate_security');
    $this->trongate_security->_make_sure_allowed();

    // Validate file upload
    if ($_FILES['picture']['name'] == '') {
        redirect($_SERVER['HTTP_REFERER']);
    }

    // Initialize basic settings
    $config = [
        'destination' => 'products_pics/'.$update_id,
        'max_width' => 800,
        'max_height' => 600,
        'upload_to_module' => true,
        'make_rand_name' => false
    ];

    try {
        // Perform the upload
        $file_info = $this->upload_picture($config);
        
        // Update database with filename
        $data['picture'] = $file_info['file_name'];
        $this->model->update($update_id, $data);
        
        set_flashdata('Picture uploaded successfully');
        redirect($_SERVER['HTTP_REFERER']);
    } catch (Exception $e) {
        set_flashdata('Upload failed: ' . $e->getMessage());
        redirect($_SERVER['HTTP_REFERER']);
    }
}
```

```php
// Example 2: Image upload with thumbnail generation
function submit_product_picture_with_thumbnail($update_id) {
    $this->module('trongate_security');
    $this->trongate_security->_make_sure_allowed();

    // Validate file upload
    if ($_FILES['picture']['name'] == '') {
        redirect($_SERVER['HTTP_REFERER']);
    }

    // Initialize settings with thumbnail configuration
    $config = [
        // Core settings
        'destination' => 'products_pics/'.$update_id,
        'max_width' => 800,
        'max_height' => 600,
        'upload_to_module' => true,
        'make_rand_name' => false,
        
        // Thumbnail settings
        'thumbnail_dir' => 'products_pics_thumbnails/'.$update_id,
        'thumbnail_max_width' => 150,
        'thumbnail_max_height' => 150
    ];

    try {
        // Perform upload with thumbnail generation
        $file_info = $this->upload_picture($config);
        
        // Update database with filename
        $data['picture'] = $file_info['file_name'];
        $this->model->update($update_id, $data);
        
        set_flashdata('Picture and thumbnail uploaded successfully');
        redirect($_SERVER['HTTP_REFERER']);
    } catch (Exception $e) {
        set_flashdata('Upload failed: ' . $e->getMessage());
        redirect($_SERVER['HTTP_REFERER']);
    }
}
```
## Best Practices

- **Security:** Always implement Trongate security checks before processing uploads
- **Validation:** Validate file types and sizes before processing
- **Directory Structure:** Ensure upload directories exist using `_make_sure_got_destination_folders()`
- **Database Storage:** Store only filenames, not full paths, in the database
- **Error Handling:** Implement proper try-catch blocks and user feedback
