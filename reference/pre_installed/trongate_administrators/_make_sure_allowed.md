# _make_sure_allowed()


public function _make_sure_allowed(): ?string

## Description

Ensures that access is allowed for administrators by verifying the presence of a valid token. If the user is not logged in or lacks the required token, they are redirected to the Trongate administrators' login page.


If accessed in development mode (ENV == 'dev') without a valid token, a token is automatically generated for the first Trongate administrator record.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not take any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| string\|null | Returns a token consisting of 32 alphanumeric characters (including uppercase letters, lowercase letters and digits) if access is granted.  If access is not granted the method returns null and redirects to the login page for adminstrators. |

## Example Usage


This method is typically accessed via the **Trongate_security** module using code similar to the following:

```php
$this->module('trongate_security');
$token = $this->trongate_security->_make_sure_allowed();
```
