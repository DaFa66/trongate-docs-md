# upload()


public function upload(array $config): array

## Description

Handles the file upload process with specified configuration. This method validates the upload configuration, processes the uploaded file, performs security checks, generates a secure filename, and moves the file to the target destination. It returns an array containing details about the uploaded file.


**How It Works:**


- The method first validates the upload configuration, ensuring all required options are provided and valid.
- It checks if a file was uploaded and validates the file's integrity and security (e.g., MIME type, memory requirements).
- A secure filename is generated, either randomly or based on the original filename, depending on the configuration.
- The file is moved to the target destination, and its details (name, path, type, size) are returned as an array.


**Note:** Ensure the upload configuration is valid and the destination path is accessible. If the upload fails due to invalid configuration, security validation, or file movement issues, an exception will be thrown.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $config | array | An associative array containing upload configuration options:<br><br>- `'destination'`: (string) The target directory for the uploaded file.<br>- `'target_module'`: (string) The target module name (defaults to the current segment).<br>- `'upload_to_module'`: (bool) Whether to upload to the module's assets directory (default: false).<br>- `'make_rand_name'`: (bool) Whether to generate a random filename (default: false). | N/A |

## Exceptions

Throws an **Exception** if:


- The upload configuration is invalid (e.g., missing destination).
- No file was uploaded or the upload failed.
- The file fails security validation (e.g., invalid MIME type or insufficient memory).
- The file cannot be moved to the target destination.
## Return Value


| Type | Description |
| ---|---|
| array | An associative array containing details about the uploaded file:<br><br>- `'file_name'`: (string) The name of the uploaded file.<br>- `'file_path'`: (string) The full path to the uploaded file.<br>- `'file_type'`: (string) The MIME type of the uploaded file.<br>- `'file_size'`: (int) The size of the uploaded file in bytes. |

## Example Usage

```
// Example 1: Uploading a file to a specific directory
try {
    $file = new File();
    $config = [
        'destination' => 'uploads/images',
        'make_rand_name' => true
    ];
    $uploaded_file = $file->upload($config);
    echo "File uploaded successfully: " . $uploaded_file['file_name'];
} catch (Exception $e) {
    echo "Upload failed: " . $e->getMessage();
}
```

```
// Example 2: Uploading a file to a module's assets directory
try {
    $file = new File();
    $config = [
        'destination' => 'profile_pictures',
        'upload_to_module' => true,
        'target_module' => 'users'
    ];
    $uploaded_file = $file->upload($config);
    echo "File uploaded to module successfully: " . $uploaded_file['file_path'];
} catch (Exception $e) {
    echo "Upload failed: " . $e->getMessage();
}
```

```
// Example 3: Handling multiple file uploads
$files_to_upload = ['file1.jpg', 'file2.png'];
foreach ($files_to_upload as $file_name) {
    try {
        $file = new File();
        $config = [
            'destination' => 'uploads/documents',
            'make_rand_name' => false
        ];
        $uploaded_file = $file->upload($config);
        echo "Uploaded: " . $uploaded_file['file_name'] . "\n";
    } catch (Exception $e) {
        echo "Error uploading $file_name: " . $e->getMessage() . "\n";
    }
}
```
## Best Practices

- **Validate Configuration:** Always ensure the upload configuration is valid and the destination path is accessible.
- **Use Random Filenames:** When handling sensitive files, use `'make_rand_name' => true` to generate random filenames and avoid conflicts.
- **Check Memory Requirements:** Ensure the server has sufficient memory to handle large file uploads.
- **Secure Uploads:** Always validate file MIME types and restrict access to sensitive directories.
- **Handle Exceptions:** Use try-catch blocks to handle exceptions gracefully, especially when uploading multiple files or working with user-provided paths.
