# flashdata()


function flashdata(string $opening_html = null, string $closing_html = null): void

## Description

Outputs a flash message stored in the session, wrapped in specified HTML tags.


If no HTML tags are provided, it defaults to displaying the message within a paragraph tag with green color.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $opening_html | string | Optional. HTML tag(s) to wrap the flash message. If not provided, defaults to `<p style="color: green;">`. | null |
| $closing_html | string | Optional. Closing HTML tag(s) if opening tag(s) are provided. If not provided, defaults to `</p>`. | null |

## Return Value


| Type | Description |
| ---|---|
| void | This function does not return anything. It directly outputs the flash message. |

## Example Usage

```
// Output flash message wrapped in custom HTML tags
flashdata('<div class="alert alert-success">', '</div>');

// Output flash message with default paragraph tags
flashdata();
```
