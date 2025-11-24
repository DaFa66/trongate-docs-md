# write()


function write(string $file_path, mixed $data, bool $append = false): bool

## Description

Writes or appends data to a file. This method ensures the file path is valid and accessible, writes the provided data to the file, and optionally appends the data instead of overwriting the file.


**How It Works:**


- The method first validates the `$file_path` to ensure it is not restricted by security rules (e.g., accessing sensitive directories like `config` or `engine`).
- If the path is valid, it writes the provided `$data` to the file using PHP's `file_put_contents()` function.
- If the `$append` flag is set to `true`, the data is appended to the file instead of overwriting it.
- If the write operation fails (e.g., due to insufficient permissions or an invalid path), an exception is thrown with a descriptive error message.


**Note:** Ensure the file path is valid and writable before calling this method. If the file is restricted or inaccessible, or if the write operation fails, an exception will be thrown.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $file_path | string | The absolute or relative path to the file where data should be written. The path must pass security validation. | N/A |
| $data | mixed | The data to write to the file. This can be a string, array, or any other data type that can be converted to a string. | N/A |
| $append | bool | Determines whether the data should be appended to the file (`true`) or overwrite the file (`false`). | false |

## Exceptions

Throws an **Exception** if:


- The `$file_path` is restricted by security rules.
- The write operation fails (e.g., due to insufficient permissions or an invalid path).
## Return Value


| Type | Description |
| ---|---|
| bool | Returns `true` if the data is successfully written to the file. If the operation fails, an exception is thrown instead of returning `false`. |

## Example Usage

```
// Example 1: Writing data to a file (overwrite)
try {
    $file = new File();
    $success = $file->write('/path/to/file.txt', 'Hello, world!');
    if ($success) {
        echo "Data written successfully.";
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 2: Appending data to a file
try {
    $file = new File();
    $success = $file->write('/path/to/file.txt', 'Appended text.', true);
    if ($success) {
        echo "Data appended successfully.";
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 3: Writing an array to a file
try {
    $file = new File();
    $data = ['line1', 'line2', 'line3'];
    $success = $file->write('/path/to/file.txt', implode("\n", $data));
    if ($success) {
        echo "Array data written successfully.";
    }
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```
## Best Practices

- **Validate Paths:** Always ensure the file path is valid and does not conflict with restricted paths before calling this method.
- **Use Append Flag Wisely:** Use the `$append` flag to avoid overwriting important data in existing files.
- **Handle Large Data:** For large data sets, consider writing data in chunks to avoid memory issues.
- **Check Permissions:** Ensure the script has sufficient permissions to write to the file and its directory.
- **Handle Exceptions:** Use try-catch blocks to handle exceptions gracefully, especially when working with user-provided paths or data.
