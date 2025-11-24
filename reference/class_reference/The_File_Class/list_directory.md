# list_directory()


function list_directory(string $directory_path, bool $recursive = false): array

## Description

Lists files and directories within a specified directory. This method returns an array containing the names of files and directories within the specified directory. It also supports recursive listing, which includes all subdirectories and their contents.


**How It Works:**


- The method first validates the `$directory_path` to ensure it is not restricted by security rules (e.g., accessing sensitive directories like `config` or `engine`).
- It checks if the specified path is a valid directory. If not, an exception is thrown.
- It iterates through the contents of the directory using PHP's `DirectoryIterator`.
- If the `$recursive` flag is set to `true`, it recursively lists the contents of subdirectories and stores them as nested arrays.
- If the `$recursive` flag is `false`, it returns a flat array of file and directory names.


**Note:** Ensure the directory exists and is accessible before calling this method. If the directory does not exist or is restricted, an exception will be thrown.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $directory_path | string | The absolute or relative path to the directory whose contents are to be listed. The path must pass security validation. | N/A |
| $recursive | bool | Determines whether the listing should be recursive. If `true`, subdirectories and their contents are included in the result. | false |

## Return Value


| Type | Description |
| ---|---|
| array | An array containing the names of files and directories within the specified directory. If `$recursive` is `true`, subdirectories are represented as nested arrays. |

## Exceptions

Throws an **Exception** if:


- The `$directory_path` is restricted by security rules.
- The specified path does not exist or is not a directory.
## Example Usage

```
// Example 1: Non-recursive listing
try {
    $file = new File();
    $contents = $file->list_directory('/path/to/directory');
    print_r($contents);
    /*
    Output:
    Array
    (
        [0] => file1.txt
        [1] => file2.jpg
        [2] => subdirectory
    )
    */
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 2: Recursive listing
try {
    $file = new File();
    $contents = $file->list_directory('/path/to/directory', true);
    print_r($contents);
    /*
    Output:
    Array
    (
        [0] => file1.txt
        [1] => file2.jpg
        [2] => subdirectory => Array
            (
                [0] => subfile1.txt
                [1] => subfile2.jpg
            )
    )
    */
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 3: Handling restricted paths
try {
    $file = new File();
    $contents = $file->list_directory('/path/to/restricted/directory');
} catch (Exception $e) {
    echo "Error: " . $e->getMessage(); // Output: "Access to this path is restricted: /path/to/restricted/directory"
}
```
## Best Practices

- **Validate Paths:** Ensure the directory path is valid and does not conflict with restricted paths before calling this method.
- **Use Recursive Flag Wisely:** Use the `$recursive` flag only when necessary, as it can significantly increase the size of the returned array for directories with many subdirectories.
- **Handle Exceptions:** Use try-catch blocks to handle exceptions gracefully, especially when working with user-provided paths.
- **Optimize for Large Directories:** For directories with a large number of files or subdirectories, consider using alternative methods (e.g., pagination) to avoid performance issues.
- **Combine with Other Methods:** Use this method in conjunction with other file operations (e.g., `info()`, `delete()`) to perform bulk operations on listed files or directories.
