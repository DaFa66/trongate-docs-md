# replace_html_tags()


function replace_html_tags(string $content, array $specifications): string

## Description

Converts HTML content based on given specifications.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $content | string | The original HTML content to be converted. | N/A |
| $specifications | array | An array containing specifications for conversion, including opening and closing strings. | N/A |

## Return Value


| Type | Description |
| ---|---|
| string | The modified HTML content. |

## Example Usage

```
$html_content = "<div class='content'><p>This is some content.</p></div>";
$specifications = [
    'opening_string_before' => '<p>',
    'close_string_before' => '</p>',
    'opening_string_after' => '<div>',
    'close_string_after' => '</div>'
];
$modified_content = replace_html_tags($html_content, $specifications);
echo $modified_content;
// Output: <div class='content'><div>This is some content.</div></div>
```
