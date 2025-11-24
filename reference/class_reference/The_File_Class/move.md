# move()


function move(string $source_path, string $destination_path): bool

## Description

Moves a file from one location to another. This method ensures the source file exists, validates the source path against predefined security rules, and attempts to move the file to the specified destination. If the move operation is successful, it returns `true`; otherwise, it throws an exception.


**How It Works:**


- The method first validates the `$source_path` to ensure it is not restricted by security rules (e.g., accessing sensitive directories like `config` or `engine`).
- It checks if the source file exists at the specified path. If the file does not exist, an exception is thrown.
- If the source file exists and the path is valid, it attempts to move the file to the `$destination_path` using PHP's `rename()` function.
- If the move operation fails (e.g., due to insufficient permissions or an invalid destination path), an exception is thrown with a descriptive error message.


**Note:** Ensure the source file exists and the destination path is writable before calling this method. If the source file is restricted or inaccessible, or if the move operation fails, an exception will be thrown.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $source_path | string | The absolute or relative path to the source file that needs to be moved. The path must pass security validation. | N/A |
| $destination_path | string | The absolute or relative path to the destination where the file will be moved. The destination directory must be writable. | N/A |

## Exceptions

Throws an **Exception** if:


- The `$source_path` is restricted by security rules.
- The source file does not exist at the specified path.
- The move operation fails (e.g., due to insufficient permissions or an invalid destination path).
## Return Value


| Type | Description |
| ---|---|
| bool | Returns `true` if the file is successfully moved. If the operation fails, an exception is thrown instead of returning `false`. |

## Example Usage

```
// Example 1: Moving a file to a new location
try {
    $file = new File();
    $success = $file->move('/path/to/source/file.txt', '/path/to/destination/file.txt');
    if ($success) {
        echo "File moved successfully.";
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 2: Moving multiple files in a loop
$files_to_move = [
    '/path/to/source/file1.txt' => '/path/to/destination/file1.txt',
    '/path/to/source/file2.jpg' => '/path/to/destination/file2.jpg',
];

$file = new File();
foreach ($files_to_move as $source => $destination) {
    try {
        $file->move($source, $destination);
        echo "Moved $source to $destination successfully.\n";
    } catch (Exception $e) {
        echo "Failed to move $source: " . $e->getMessage() . "\n";
    }
}
```

```
// Example 3: Handling restricted paths
try {
    $file = new File();
    $file->move('/path/to/restricted/file.txt', '/path/to/destination/file.txt');
} catch (Exception $e) {
    echo "Error: " . $e->getMessage(); // Output: "Access to this path is restricted: /path/to/restricted/file.txt"
}
```
## Best Practices

- **Validate Paths:** Always ensure the source and destination paths are valid and do not conflict with restricted paths before calling this method.
- **Check File Existence:** Verify the source file exists before attempting to move it, or handle the exception gracefully.
- **Ensure Permissions:** Make sure the script has sufficient permissions to read the source file and write to the destination directory.
- **Handle Exceptions:** Use try-catch blocks to handle exceptions, especially when moving multiple files or working with user-provided paths.
- **Backup Important Files:** Before moving critical files, consider creating backups to prevent data loss in case of errors.
