# get_status_codes()


public function get_status_codes(?int $status_code = null): array|string|null

## Description

Retrieves HTTP status codes and their descriptions. This method provides a mapping of HTTP status codes to their respective descriptions. If a specific status code is provided, the corresponding description is returned as a string. If no status code is provided, an array containing all HTTP status codes and descriptions is returned. If the provided status code is not found, "Unknown HTTP Response Code" is returned.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $status_code | int\|null | The HTTP status code to retrieve the description for. Defaults to null. | null | No |

## Return Value


| Type | Description |
| ---|---|
| array\|string\|null | If a specific status code is provided, returns its description as a string. If no status code is provided, returns an array of all HTTP status codes and descriptions. If the provided status code is not found, returns "Unknown HTTP Response Code". |

## Example Usage

```
// Example Usage not available for this method
```
