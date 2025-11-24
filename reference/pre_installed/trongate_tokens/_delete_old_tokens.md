# _delete_old_tokens()


public function _delete_old_tokens(?int $user_id = null): void

## Description

Deletes old tokens from the database. This function deletes tokens that have expired. If a user ID is provided, it also deletes tokens associated with that user.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $user_id | int\|null | Optional user ID to delete tokens for a specific user. | null | No |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return any value. |

## Example Usage

```php
$this->module('trongate_tokens');
$this->trongate_tokens->_delete_old_tokens();
```
