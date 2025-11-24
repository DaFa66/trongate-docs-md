# _generate_token()


public function _generate_token(array $data): string

## Description

Generates a token based on provided data. The token is a 32-character random string that can be optionally set as a cookie and has an optional expiration date.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $data['user_id'] | int | The user's Trongate user ID. | None | Yes |
| $data['expiry_date'] | int | Unix timestamp for token expiration. | time() + $this->default_token_lifespan | No |
| $data['set_cookie'] | bool | If true, set the token as a cookie. | false | No |

## Return Value


| Type | Description |
| ---|---|
| string | The generated token. |

## Example Usage


In the code sample below, a token is generated for a user with ID 1, with an expiration date set, and the token is also set as a cookie.

```php
$data = [
    'user_id' => 1,
    'expiry_date' => time() + 3600, // 1 hour from now
    'set_cookie' => true
];

$this->module('trongate_tokens');
$token = $this->trongate_tokens->_generate_token($data);
```
