# truncate_words()


function truncate_words(string $value, int $max_words): string

## Description

Truncates a string to a specified maximum number of words. If the number of words in the string exceeds the maximum, the string is shortened to the maximum number of words and an ellipsis (...) is appended.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $value | string | The input string to be truncated. | N/A |
| $max_words | int | The maximum number of words allowed in the truncated string. | N/A |

## Return Value


| Type | Description |
| ---|---|
| string | Returns the truncated string with an ellipsis (...) if the original string's word count exceeds the maximum allowed. |

## Example Usage

```
echo truncate_words("Hello World! This is a Test String for example purposes.", 5);
// Output: Hello World! This is a...
```
