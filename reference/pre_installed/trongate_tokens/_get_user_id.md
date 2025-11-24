# _get_user_id()


public function _get_user_id(?string $token = null): int|false

## Description

Retrieves the Trongate user ID based on a provided token. If no token is provided, the method attempts to fetch and use a token from the session, cookie, or page header values. If no valid token is found, the method returns false.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $token | string\|null | Optional. The token to retrieve the user ID for. | null | No |

## Return Value


| Type | Description |
| ---|---|
| int\|false | The Trongate user ID if found, or false if not found. |

## Example Usage #1


In the code sample below, a token is passed into the **_get_user_id()** method in an attempt to return a Trongate user ID.

```php
$token = 'agFauQmexzstRnBmKv5BNDgewsWgD32j';
$this->module('trongate_tokens');
$trongate_user_id = $this->trongate_tokens->_get_user_id($token);
```
## Example Usage #2


In this alternative example, no token has been passed into the **_get_user_id()** method. This means that the method will attempt to retrieve a token from the session, cookie, or page header values. If a valid token is found in any of those locations, the method will then attempt to fetch and return an associated Trongate user ID.

```php
$this->module('trongate_tokens');
$trongate_user_id = $this->trongate_tokens->_get_user_id();
```
