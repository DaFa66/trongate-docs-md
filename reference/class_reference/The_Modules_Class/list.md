# list()


function list(bool $recursive = false): array

## Description

Lists all existing modules.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $recursive | bool | Optional. Determines whether the listing should be recursive. Default is false. | false |

## Return Value


| Type | Description |
| ---|---|
| array | Returns an array containing the list of existing modules. |

## Example Usage

```php
$existing_modules = $this->modules->list(true);
json($existing_modules);
// Output: Array containing the list of existing modules
```
