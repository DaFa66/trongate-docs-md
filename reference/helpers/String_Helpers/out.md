# out()


function out(?string $input, string $encoding = 'UTF-8', string $output_format = 'html'): string

## Description

Safely escapes and formats a string for various output contexts, providing protection against cross-site scripting (XSS) attacks and ensuring proper encoding for different output formats.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $input | string\|null | The string to be escaped. If null, it will be treated as an empty string. |
| $encoding | string | (optional) The character encoding to use for escaping. Default is 'UTF-8'. |
| $output_format | string | (optional) The desired output format. Possible values are 'html' (default), 'xml', 'json', 'javascript', or 'attribute'. |

## Return Value


| Type | Description |
| ---|---|
| string | The escaped and formatted string ready for safe inclusion in the specified context. |

## Example #1: Basic HTML Output


The code sample below demonstrates the basic usage of the `out` function for HTML output. This is particularly useful when displaying user-generated content on a webpage, such as comments or forum posts, where you need to prevent potential XSS attacks.

```
$input = '<script>alert("XSS Attack")</script>';
echo out($input); 

// Output:  &lt;script&gt;alert("XSS Attack")&lt;/script&gt;
```

## Example #2: XML Output


This example shows how to use the `out` function for XML output. This is useful when generating XML data, such as when creating RSS feeds or SOAP responses, where proper XML escaping is crucial for maintaining valid XML structure.

```
$input = '<title>Example & "Sample"</title>';
echo out($input, 'UTF-8', 'xml'); 

// Output:  &lt;title&gt;Example &amp; "Sample"&lt;/title&gt;
```

## Example #3: JSON Output


This example demonstrates using the `out` function for JSON output. This is particularly relevant when working with APIs or AJAX requests where you need to ensure that the JSON data is properly escaped and formatted for JavaScript consumption.

```
$input = '"Special" characters: <>&';
echo out($input, 'UTF-8', 'json'); 

// Output:  \"Special\" characters: <>&
```

## Example #4: JavaScript Output


This example shows how to use the `out` function for JavaScript output. This is useful when you need to embed PHP variables directly into JavaScript code, ensuring that the output is properly escaped for use in a script context.

```
$input = 'John Doe';
echo '<script>let name = "' . out($input, 'UTF-8', 'javascript') . '";</script>';

// Output:  &lt;script&gt;let name = "John Doe";&lt;/script&gt;
```

## Example #5: HTML Attribute Output


This example demonstrates using the `out` function for HTML attribute output. This is crucial when dynamically generating HTML attributes, such as when creating data attributes or setting element styles based on user input or database values.

```
$input = 'Click "here"';
echo '<a href="#" title="' . out($input, 'UTF-8', 'attribute') . '">Link</a>';

// Output:  &lt;a href="#" title="Click &quot;here&quot;"&gt;Link&lt;/a&gt;
```

## Notes


- The function automatically handles null input by treating it as an empty string.
- For 'html' and 'attribute' output formats, both single and double quotes are escaped.
- The 'xml' output format uses the ENT_XML1 flag for XML-specific escaping.
- The 'json' and 'javascript' output formats use json_encode() with additional flags to ensure proper escaping of special characters.
- An Exception will be thrown if an unsupported output format is provided.
- This function is crucial for preventing XSS attacks and should be used whenever outputting user-supplied data.
