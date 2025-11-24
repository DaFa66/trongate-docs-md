# return_file_info()


function return_file_info(string $file_string): array

## Description

Extracts file name and extension from a given file path.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $file_string | string | The file path from which to extract information. | N/A |

## Return Value


| Type | Description |
| ---|---|
| array | An associative array containing the 'file_name' and 'file_extension'. |

## Example Usage

```
$file_info = return_file_info("/path/to/your/file.jpg");
echo "File Name: " . $file_info['file_name'] . "\n";
echo "File Extension: " . $file_info['file_extension'] . "\n";
// Output:
// File Name: file
// File Extension: .jpg
```
