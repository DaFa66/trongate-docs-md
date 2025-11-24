# validation_errors()


function validation_errors(?string $opening_html = null, ?string $closing_html = null): ?string

## Description

Retrieves and displays validation error messages, if any, from the session. Error messages can be wrapped in custom HTML tags specified by the caller. If no HTML tags are specified, and constants ERROR_OPEN and ERROR_CLOSE are defined, these are used; otherwise, it defaults to paragraph tags with red text color.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $opening_html | string\|null | Optional. The opening HTML tag to use for each error message. | null |
| $closing_html | string\|null | Optional. The closing HTML tag to use after each error message. | null |

## Return Value


| Type | Description |
| ---|---|
| string\|null | Returns formatted validation error messages if any exist; otherwise, returns null if no errors are found. |

## Example Usage

```
echo validation_errors('<div class="error-message">', '</div>');
// Output might be something like:
// <div class="error-message">Field must not be empty</div>
// <div class="error-message">Username must be at least 6 characters long</div>
```
