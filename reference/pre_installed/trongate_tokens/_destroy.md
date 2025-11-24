# _destroy()


public function _destroy(): void

## Description

Destroys tokens from session, cookie, and HTTP headers. This method removes tokens from session, cookie, and HTTP headers storage, and deletes them from the database. Additionally, it cleans up expired tokens from the database.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not take any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return any value. |

## Example Usage

```php
$this->module('trongate_tokens');
$this->trongate_tokens->_destroy();
```
