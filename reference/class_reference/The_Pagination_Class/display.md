# display()


public static function display(array $pagination_data): void

## Description

Displays pagination links based on provided pagination data. The method automatically detects page numbers and pagination roots if not explicitly specified.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $pagination_data | array | The pagination data array. | N/A |

## Required Array Keys


| Key | Type | Description |
| ---|---|---|
| total_rows | int | The total number of records available. |
| limit | int | The maximum number of records per page. |
| record_name_plural | string | The plural label for the records. |

## Optional Array Keys


| Key | Type | Description | Default |
| ---|---|---|---|
| page_num_segment | int | The URL segment number indicating the current page. | Auto-detected from the last URL segment if numeric |
| pagination_root | string | The base URL for pagination links. | Auto-detected from current URL |
| include_showing_statement | bool | Whether to display a "Showing x to y of z" statement. | false |
| include_css | bool | Whether to include default pagination styles. | false |
| num_links_per_page | int | The number of pagination links to display. | 10 |
| settings | array | Custom pagination settings for HTML output. | Default settings array |

## Return Value


| Type | Description |
| ---|---|
| void | No return value. The method outputs HTML directly. |

## Example Usage

### Minimal Configuration (Using Auto-detection)

```php
<?php 
// Controller
$pagination_data = [
  'total_rows' => count($rows),
  'limit' => 10,
  'record_name_plural' => 'books',
  'include_showing_statement' => true
];
$data['pagination_data'] = $pagination_data;

// View file
Pagination::display($pagination_data);
?>
```
### Explicit Configuration

```php
<?php 
// Controller
$pagination_data = [
  'total_rows' => count($rows),
  'limit' => 10,
  'record_name_plural' => 'books',
  'page_num_segment' => 3,
  'pagination_root' => 'books/manage',
  'include_showing_statement' => true,
  'include_css' => true
];
$data['pagination_data'] = $pagination_data;

// View file
Pagination::display($pagination_data);
?>
```
