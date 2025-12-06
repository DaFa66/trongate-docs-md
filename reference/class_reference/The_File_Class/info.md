# info()


function info(string $file_path): array

## Description

Retrieves metadata about a file, including its name, size, last modification time, permissions, MIME type, and human-readable size. This method is useful for gathering detailed information about a file for logging, debugging, or display purposes.


**How It Works:**


- The method first checks if the file exists at the specified path. If the file does not exist, an exception is thrown.
- If the file exists, it retrieves the following metadata:

- **File Name:** The base name of the file (e.g., `file.txt`).
- **Size:** The size of the file in bytes.
- **Human-Readable Size:** The size of the file formatted in a human-readable format (e.g., `1.23 MB`).
- **Modified Time:** The last modification time of the file as a Unix timestamp.
- **Permissions:** The file permissions in octal notation (e.g., `0644`).
- **Readable Permissions:** The file permissions formatted for readability (e.g., `0644`).
- **MIME Type:** The MIME type of the file (e.g., `text/plain`).


- The metadata is returned as an associative array.


**Note:** Ensure the file exists and is accessible before calling this method. If the file does not exist, an exception will be thrown.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $file_path | string | The absolute or relative path to the file for which metadata should be retrieved. | N/A |

## Return Value


| Type | Description |
| ---|---|
| array | An associative array containing the following metadata:<br><br>- `file_name`: (string) The base name of the file.<br>- `size`: (int) The size of the file in bytes.<br>- `human_readable_size`: (string) The size of the file in a human-readable format.<br>- `modified_time`: (int) The last modification time as a Unix timestamp.<br>- `permissions`: (int) The file permissions in octal notation.<br>- `readable_permissions`: (string) The file permissions formatted for readability.<br>- `mime_type`: (string) The MIME type of the file. |

## Exceptions

Throws an **Exception** if:


- The file does not exist at the specified path.
## Example Usage

```
// Example 1: Retrieving metadata for a file
try {
    $file = new File();
    $file_info = $file->info('/path/to/file.txt');
    print_r($file_info);
    /*
    Output:
    Array
    (
        [file_name] => file.txt
        [size] => 1024
        [human_readable_size] => 1.00 KB
        [modified_time] => 1698765432
        [permissions] => 33188
        [readable_permissions] => 0644
        [mime_type] => text/plain
    )
    */
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 2: Displaying human-readable file size
try {
    $file = new File();
    $file_info = $file->info('/path/to/large_file.zip');
    echo "File size: " . $file_info['human_readable_size']; // Output: "File size: 123.45 MB"
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 3: Checking file permissions
try {
    $file = new File();
    $file_info = $file->info('/path/to/protected_file.txt');
    echo "File permissions: " . $file_info['readable_permissions']; // Output: "File permissions: 0644"
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```
## Best Practices

- **Validate Paths:** Ensure the file path is valid and does not conflict with restricted paths before calling this method.
- **Handle Exceptions:** Use try-catch blocks to handle exceptions gracefully, especially when working with user-provided paths.
- **Use for Debugging:** This method is useful for debugging or logging file-related issues, such as permission errors or missing files.
- **Combine with Other Methods:** Use this method in conjunction with other file operations (e.g., `read()`, `write()`) to ensure the file is accessible and has the expected metadata.
