# download()


function download(string $file_path, bool $as_attachment = true): void

## Description

Initiates a file download or displays it inline in the browser. This method prepares and sends the appropriate HTTP headers to either force a file download or display the file directly in the browser, depending on the `$as_attachment` parameter.


**How It Works:**


- The method first validates the `$file_path` to ensure it is not restricted by security rules (e.g., accessing sensitive directories like `config` or `engine`).
- It checks if the file exists and is readable. If the file is inaccessible or does not exist, an exception is thrown.
- If the file is valid, it clears any output buffers to prevent interference with the file download.
- It sets the appropriate HTTP headers based on the `$as_attachment` parameter:
        
- If `$as_attachment` is `true`, the browser will prompt the user to download the file.
- If `$as_attachment` is `false`, the file will be displayed inline in the browser (if supported by the file type).


      
- The file is then read and sent to the output buffer using `readfile()`.
- The script terminates immediately after sending the file to prevent additional output.


**Note:** Ensure the file exists and is accessible before calling this method. If the file is restricted, inaccessible, or does not exist, an exception will be thrown.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $file_path | string | The absolute or relative path to the file that needs to be downloaded or displayed. The path must pass security validation. | N/A |
| $as_attachment | bool | Determines whether the file should be downloaded as an attachment (`true`) or displayed inline (`false`). | true |

## Exceptions

Throws an **Exception** if:


- The `$file_path` is restricted by security rules (e.g., accessing sensitive directories).
- The file does not exist at the specified path.
- The file is not readable or accessible.
## Return Value

**void**


This method does not return a value. It sends the file to the browser and terminates the script.
## Example Usage

```
// Example 1: Force downloading a file
try {
    $file = new File();
    $file->download('/path/to/file.pdf');
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 2: Displaying a file inline in the browser
try {
    $file = new File();
    $file->download('/path/to/image.jpg', false);
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

```
// Example 3: Handling restricted paths
try {
    $file = new File();
    $file->download('/path/to/restricted/file.txt');
} catch (Exception $e) {
    echo "Error: " . $e->getMessage(); // Output: "Access to this file is restricted: /path/to/restricted/file.txt"
}
```
## Best Practices

- **Validate Paths:** Always ensure the file path is valid and does not conflict with restricted paths before calling this method.
- **Check File Accessibility:** Verify the file exists and is readable before attempting to download or display it.
- **Use Appropriate Headers:** Set the `$as_attachment` parameter based on the desired behavior (download or inline display).
- **Handle Exceptions:** Use try-catch blocks to handle exceptions gracefully, especially when working with user-provided paths.
- **Terminate Script:** Ensure no additional output is sent after calling this method, as it terminates the script to prevent interference with the file download.
