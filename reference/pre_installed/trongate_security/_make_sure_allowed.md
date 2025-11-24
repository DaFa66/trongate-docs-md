# _make_sure_allowed()


function _make_sure_allowed(string $scenario = 'admin panel'): string

## Description

Ensures the user is allowed access for the specified scenario.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $scenario | string | Optional. The scenario for access control. | admin panel |

## Return Value


| Type | Description |
| ---|---|
| string | Returns a (trongate) token or initializes the 'not allowed' procedure. |

## Example Usage #1

```php
$this->module('trongate_security');
$token = $this->trongate_security->_make_sure_allowed();
```
## Example Usage #2

```php
$this->module('trongate_security');
$this->trongate_security->_make_sure_allowed('members area');
```
