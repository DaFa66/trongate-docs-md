# redirect()


function redirect(string $target_url): void

## Description

Perform an HTTP redirect to the specified URL.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $target_url | string | The URL to which the redirect should occur. |

## Return Value


This function does not return a value.

## Example Usage

```
redirect("/login");
// Redirects the user to the login page.

redirect("https://example.com");
// Redirects the user to https://example.com.
```
