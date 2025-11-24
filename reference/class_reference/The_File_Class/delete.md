# delete()


function delete(string $file_path): bool

## Description

Deletes a file from the filesystem. This method ensures the file exists, validates the file path against predefined security rules, and attempts to delete the file. If the deletion is successful, it returns `true`; otherwise, it throws an exception.


**How It Works:**


- The method first validates the `$file_path` to ensure it is not restricted by security rules (e.g., accessing sensitive directories like `config` or `engine`).
- It checks if the file exists at the specified path. If the file does not exist, an exception is thrown.
- If the file exists and the path is valid, it attempts to delete the file using the `unlink()` function.
- If the deletion fails (e.g., due to insufficient permissions or a locked file), an exception is thrown with a descriptive error message.


**Note:** Ensure the file exists and the path is valid before calling this method. If the file is restricted or inaccessible, or if the deletion fails, an exception will be thrown.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $file_path | string | The absolute or relative path to the file that needs to be deleted. The path must pass security validation. | N/A |

## Exceptions

Throws an **Exception** if:


- The `$file_path` is restricted by security rules (e.g., accessing sensitive directories).
- The file does not exist at the specified path.
- The file cannot be deleted (e.g., due to insufficient permissions or a locked file).
## Return Value


| Type | Description |
| ---|---|
| bool | Returns `true` if the file is successfully deleted. If the operation fails, an exception is thrown instead of returning `false`. |

## Example Usage

```
// Example 1: Deleting a single file
try {
    $file = new File();
    $success = $file->delete('/path/to/file.txt');
    if ($success) {
        echo "File deleted successfully.";
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 2: Deleting multiple files in a loop
$files_to_delete = [
    '/path/to/file1.txt',
    '/path/to/file2.jpg',
    '/path/to/file3.log',
];

$file = new File();
foreach ($files_to_delete as $file_path) {
    try {
        $file->delete($file_path);
        echo "Deleted $file_path successfully.\n";
    } catch (Exception $e) {
        echo "Failed to delete $file_path: " . $e->getMessage() . "\n";
    }
}
```

```
// Example 3: Handling restricted paths
try {
    $file = new File();
    $file->delete('/path/to/restricted/file.txt');
} catch (Exception $e) {
    echo "Error: " . $e->getMessage(); // Output: "Access to this file is restricted: /path/to/restricted/file.txt"
}
```
## Best Practices

- **Validate Paths:** Always ensure the file path is valid and does not conflict with restricted paths before calling this method.
- **Check File Existence:** Verify the file exists before attempting to delete it, or handle the exception gracefully.
- **Handle Exceptions:** Use try-catch blocks to handle exceptions, especially when deleting multiple files or working with user-provided paths.
- **Ensure Permissions:** Make sure the script has sufficient permissions to delete the file.
- **Log Deletions:** For auditing purposes, log successful and failed deletion attempts.
