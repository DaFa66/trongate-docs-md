# _get_user_level()


public function _get_user_level(?string $token = null): string|false

## Description

Retrieves the user level associated with the given token or the current user token. If a token is provided, it retrieves the user level for that token. If no token is provided, it retrieves the user level for the current user.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $token | string\|null | The token used to identify the user. If not provided, the token of the current user is used. | null | No |

## Return Value


| Type | Description |
| ---|---|
| string\|false | The user level title if found, otherwise false. |

## Example Usage

```php
$this->module('trongate_tokens');
$user_level = $this->trongate_tokens->_get_user_level();
echo $user_level;  // This will output something like 'admin'
```
