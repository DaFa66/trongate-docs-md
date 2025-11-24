# _create_user()


function _create_user(int $user_level_id): int

## Description

Creates a new trongate user record with a specified user level ID.


Please note that this method cannot be invoked directly via the URL and is designed to be invoked by other modules, such as the Trongate Administrators module.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $user_level_id | int | The user level ID for the new user. | N/A |

## Return Value


| Type | Description |
| ---|---|
| int | The Trongate user ID of the newly created user. |

## Example Usage

```php
$this->module('trongate_users');
$trongate_user_id = $this->trongate_users->_create_user(3);
```
