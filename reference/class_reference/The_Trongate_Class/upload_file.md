# upload_file()


protected function upload_file(array $config): ?array

## Description

Uploads a file using the `upload` method from the `File` class. This method serves as a simplified way to invoke the `File` class's upload functionality within the `Trongate` framework.


**How It Works:**


- It instantiates a `File` object.
- It calls the `upload` method of the `File` class, passing the provided `$config` array as an argument.
- The `upload` method handles the file upload process, including validation, security checks, and moving the file to the target destination.
- If the upload is successful, it returns an array containing details about the uploaded file. If the upload fails, it throws an exception.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $config | array | An associative array containing upload configuration options. These options are passed directly to the `File` class's `upload` method. For details, refer to the `File` class documentation. | N/A |

## Return Value


| Type | Description |
| ---|---|
| array\|null | Returns an associative array containing details about the uploaded file if the operation is successful. The array includes:<br><br>- `file_name`: (string) The name of the uploaded file.<br>- `file_path`: (string) The full path to the uploaded file.<br>- `file_type`: (string) The MIME type of the uploaded file.<br>- `file_size`: (int) The size of the uploaded file in bytes.<br><br><br>          If the upload fails, an exception is thrown, and no value is returned. |

## Example Usage

```php
// Example: Uploading a PDF file with custom configuration
$config = [
    'destination' => 'documents/uploads/',
    'upload_to_module' => false,
    'make_rand_name' => true
];

try {
    $file_info = $this->upload_file($config);
    print_r($file_info);
    /*
    Output:
    Array
    (
        [file_name] => random_filename.pdf
        [file_path] => /path/to/documents/uploads/random_filename.pdf
        [file_type] => application/pdf
        [file_size] => 512000
    )
    */
} catch (Exception $e) {
    echo "Upload failed: " . $e->getMessage();
}
```
## Best Practices

- **Validate Configuration:** Ensure the upload configuration is valid and the destination path is accessible before calling this method.
- **Use Random Filenames:** When handling sensitive files, use `'make_rand_name' => true` to generate random filenames and avoid conflicts.
- **Handle Exceptions:** Use try-catch blocks to handle exceptions gracefully, especially when working with user-provided paths.
