# remove_query_string()


function remove_query_string(string $string): string

## Description

Remove query string from a URL.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $string | string | The URL with a query string to be processed. | N/A |

## Return Value


| Type | Description |
| ---|---|
| string | The URL without the query string. |

## Example Usage

```
echo remove_query_string("https://example.com/page?param=value");
// Output: https://example.com/page
```
