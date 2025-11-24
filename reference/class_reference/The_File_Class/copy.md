# copy()


function copy(string $source_path, string $destination_path): bool

## Description

Copies a file from a source location to a specified destination. This method ensures the source file exists and is accessible, validates the source path against predefined security rules, and performs the copy operation. If the operation succeeds, it returns `true`; otherwise, it throws an exception.


**How It Works:**


- The method first validates the `$source_path` to ensure it is not restricted by security rules (e.g., accessing sensitive directories like `config` or `engine`).
- It checks if the source file exists at the specified path.
- If both checks pass, it attempts to copy the file to the `$destination_path`.
- If the copy operation fails, an exception is thrown with a descriptive error message.


**Note:** Ensure the source file exists and the destination path is writable. If the source file is restricted or inaccessible, or if the destination path is invalid, the method will throw an exception.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $source_path | string | The absolute or relative path to the source file that needs to be copied. The path must pass security validation. | N/A |
| $destination_path | string | The absolute or relative path to the destination where the file will be copied. The destination directory must be writable. | N/A |

## Exceptions

Throws an **Exception** if:


- The `$source_path` is restricted by security rules (e.g., accessing sensitive directories).
- The source file does not exist at the specified path.
- The copy operation fails (e.g., due to insufficient permissions or an invalid destination path).
## Return Value


| Type | Description |
| ---|---|
| bool | Returns `true` if the file is successfully copied. If the operation fails, an exception is thrown instead of returning `false`. |

## Example Usage

```
// Example 1: Copying a file to a new location
try {
    $file = new File();
    $success = $file->copy('/path/to/source/file.txt', '/path/to/destination/file.txt');
    if ($success) {
        echo "File copied successfully.";
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 2: Copying multiple files in a loop
$files_to_copy = [
    '/path/to/source/file1.txt' => '/path/to/destination/file1.txt',
    '/path/to/source/file2.jpg' => '/path/to/destination/file2.jpg',
];

$file = new File();
foreach ($files_to_copy as $source => $destination) {
    try {
        $file->copy($source, $destination);
        echo "Copied $source to $destination successfully.\n";
    } catch (Exception $e) {
        echo "Failed to copy $source: " . $e->getMessage() . "\n";
    }
}
```

```
// Example 3: Handling restricted paths
try {
    $file = new File();
    $file->copy('/path/to/restricted/file.txt', '/path/to/destination/file.txt');
} catch (Exception $e) {
    echo "Error: " . $e->getMessage(); // Output: "Access to this path is restricted: /path/to/restricted/file.txt"
}
```
## Best Practices

- **Validate Paths:** Always ensure the source and destination paths are valid and accessible before calling this method.
- **Handle Exceptions:** Use try-catch blocks to handle exceptions gracefully, especially when copying multiple files or working with user-provided paths.
- **Check Permissions:** Ensure the destination directory is writable to avoid copy failures.
- **Use Secure Paths:** Avoid copying files to or from restricted directories (e.g., `config`, `engine`) to maintain application security.
