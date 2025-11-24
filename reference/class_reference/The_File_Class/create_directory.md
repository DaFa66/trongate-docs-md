# create_directory()


function create_directory(string $directory_path, int $permissions = 0755, bool $recursive = true): bool

## Description

Creates a new directory at the specified path. This method allows for the creation of nested directories if they do not exist. It also ensures the directory path is valid and accessible based on predefined security rules.


**How It Works:**


- The method first checks if the directory already exists at the specified path. If it does, it returns `true` immediately.
- It validates the `$directory_path` to ensure it is not restricted by security rules (e.g., accessing sensitive directories like `config` or `engine`).
- If the path is valid, it attempts to create the directory with the specified permissions and recursive flag.
- If the directory creation fails, an exception is thrown with a descriptive error message.


**Note:** Ensure the directory path is valid and does not conflict with restricted paths. If the directory already exists, the method will return `true` without attempting to create it again.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $directory_path | string | The absolute or relative path where the directory should be created. The path must pass security validation. | N/A |
| $permissions | int | The permissions to set for the directory, in octal notation (e.g., `0755`). This determines the access rights for the directory. | 0755 |
| $recursive | bool | Whether to create nested directories if necessary. If set to `true`, all required parent directories will also be created. | true |

## Exceptions

Throws an **Exception** if:


- The `$directory_path` is restricted by security rules (e.g., accessing sensitive directories).
- The directory cannot be created (e.g., due to insufficient permissions or an invalid path).
## Return Value


| Type | Description |
| ---|---|
| bool | Returns `true` if the directory is successfully created or already exists. If the operation fails, an exception is thrown instead of returning `false`. |

## Example Usage

```
// Example 1: Creating a directory with default permissions and recursive flag
try {
    $file = new File();
    $success = $file->create_directory('/path/to/new_directory');
    if ($success) {
        echo "Directory created or already exists.";
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 2: Creating a directory with custom permissions and non-recursive flag
try {
    $file = new File();
    $success = $file->create_directory('/path/to/new_directory', 0777, false);
    if ($success) {
        echo "Directory created or already exists.";
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 3: Handling restricted paths
try {
    $file = new File();
    $file->create_directory('/path/to/restricted/directory');
} catch (Exception $e) {
    echo "Error: " . $e->getMessage(); // Output: "Access to this path is restricted: /path/to/restricted/directory"
}
```
## Best Practices

- **Validate Paths:** Always ensure the directory path is valid and does not conflict with restricted paths before calling this method.
- **Use Recursive Flag:** Set `$recursive` to `true` when creating nested directories to avoid errors due to missing parent directories.
- **Set Appropriate Permissions:** Use secure permissions (e.g., `0755`) to prevent unauthorized access to the directory.
- **Handle Exceptions:** Use try-catch blocks to handle exceptions gracefully, especially when working with user-provided paths.
