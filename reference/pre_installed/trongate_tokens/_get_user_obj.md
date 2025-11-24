# _get_user_obj()


public function _get_user_obj(?string $token = null): object|false

## Description

Retrieves the Trongate user object based on a provided token. If no token is provided, the method attempts to fetch and use a token from the session, cookie, or page header values. If no valid token is found, the method returns false.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $token | string\|null | Optional. The token to use for fetching the user object. | null | No |

## Return Value


| Type | Description |
| ---|---|
| object\|false | The Trongate user object if found, or false if not found. |

## Sample Data


When a valid token is found, the method will return an object.  The JSON string below shows an example of the kind of data that can be expected, within a returned object, when a valid token is found:

```
{
    "trongate_user_code": "Tz8tehsWsTPUHEtzfbYjXzaKNqLmfAUz",
    "user_level_id": 1,
    "user_level": "admin",
    "token": "CmtMsmUWxEPeXkafsdDwsfHY87ax9ku4",
    "trongate_user_id": 1,
    "expiry_date": 1716918038
}
```
## Example Usage #1


In the code sample below, a token is passed into the **_get_user_obj()** method in an attempt to return a Trongate user object.

```php
$token = 'agFauQmexzstRnBmKv5BNDgewsWgD32j';
$this->module('trongate_tokens');
$trongate_user_obj = $this->trongate_tokens->_get_user_obj($token);
```
## Example Usage #2


In this alternative example, no token has been passed into the **_get_user_obj()** method. This means that the method will attempt to retrieve a token from the session, cookie, or page header values. If a valid token is found in any of those locations, the method will then attempt to fetch and return an associated Trongate user object.

```php
$this->module('trongate_tokens');
$trongate_user_obj = $this->trongate_tokens->_get_user_obj();
```
