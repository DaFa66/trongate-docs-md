# extract_content()


function extract_content(string $string, string $start_delim, string $end_delim): string

## Description

Extracts a substring from a given string, defined by start and end delimiters. The function searches for the first occurrence of the start delimiter and the first subsequent occurrence of the end delimiter, then returns the text found between them. If either delimiter is not found, or if they are in the wrong order, an empty string is returned.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $string | string | The full string from which to extract content. | N/A | Yes |
| $start_delim | string | The starting delimiter of the content to extract. | N/A | Yes |
| $end_delim | string | The ending delimiter of the content to extract. | N/A | Yes |

## Return Value


| Type | Description |
| ---|---|
| string | The content found between the specified delimiters, or an empty string if no content is found. |

## Example Usage

```php
$string = "Hello, start here and end here, thanks.";
$start_delim = "start here";
$end_delim = "end here";
$extracted = $this->extract_content($string, $start_delim, $end_delim);
// $extracted will be " and "
```
