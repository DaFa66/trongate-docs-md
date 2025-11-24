# remove_html_code()


function remove_html_code(string $content, string $opening_pattern, string $closing_pattern): string

## Description

Removes code sections from HTML content based on specified start and end patterns.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $content | string | The original HTML content to be processed. | N/A |
| $opening_pattern | string | The pattern specifying the start of the code section to remove. | N/A |
| $closing_pattern | string | The pattern specifying the end of the code section to remove. | N/A |

## Return Value


| Type | Description |
| ---|---|
| string | The HTML content with specified code sections removed. |

## Example Usage

```php
$html_content = "<html><head></head><body><?php echo 'This is PHP code'; ?></body></html>";
$cleaned_content = remove_html_code($html_content, '<?php', '?>');
echo $cleaned_content;
// Output: <html><head></head><body></body></html>
```
