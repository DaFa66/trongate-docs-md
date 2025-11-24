# url_title()


function url_title(string $value, bool $transliteration = true): string

## Description

Converts a string into a URL-friendly slug format. This function will transliterate the string to ASCII if the 'intl' extension is loaded and transliteration is set to true, converts any non-alphanumeric characters to dashes, trims them from the start and end, and converts everything to lowercase.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $value | string | The string to be converted into a slug. | N/A |
| $transliteration | bool | Optional. Whether to transliterate characters to ASCII, enhancing compatibility with the 'intl' extension. | true |

## Return Value


| Type | Description |
| ---|---|
| string | Returns the slugified version of the string, or the original string in lowercase with non-alphanumeric characters replaced by dashes if transliteration is not applied. |

## Example Usage

```
echo url_title("Hello World! This is a Test String.");
// Output: hello-world-this-is-a-test-string
```
