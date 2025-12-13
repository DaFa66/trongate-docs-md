# Understanding The File Class


The Trongate [File class](documentation-ref/list_refs/class_reference/the-file-class) provides a comprehensive suite of methods for efficient and secure file management within your application. This class supports functionalities like uploading, deleting, reading, writing files, and managing directories. Access restrictions are in place to prevent unauthorized access to critical directories such as 'config', 'engine', and 'templates', as well as any files directly under the root application level (e.g., '.htaccess').

## Getting Started


To use the Trongate File class, you need to instantiate the class and then call its methods. Here’s a basic example of how to use the read() method:

```php
$file = new File();

try {
    $file_path = APPPATH.'public/uploads/example.txt';
    $content = $file->read($file_path);
    echo "File content: " . out($content);
} catch (Exception $e) {
    echo "Error: " . $e->getMessage();
}
```

> [!NOTE]
> **Just To Let You Know...**
>
> In the above example, the `APPPATH` constant is used to return the absolute file path of the application's root directory.  Additional information about this and other helpful features are available [from here](../0120Helpers_Explained/0080other_helpful_features.md).
> 
> 
> The example also uses Trongate's out() function to remove potentially dangerous characters from rendered output.


## Available Methods


Below is a table listing all the available methods in the Trongate File class, along with a brief description of each method:


| Method | Description |
| ---|---|
| copy() | Copies a file from one location to another. |
| create_directory() | Creates a new directory at the specified path. |
| delete() | Deletes a file from the filesystem. |
| download() | Initiates a file download or displays inline from the server or an external URL. |
| exists() | Checks whether a file or directory exists at the specified path. |
| info() | Retrieves metadata about a file. |
| list_directory() | Lists files and directories within a specified directory. |
| move() | Moves a file from one location to another. |
| read() | Reads the contents of a file. |
| upload() | Handles the file upload process with specified configuration. |
| write() | Writes or appends data to a file. |

