# login_check()


public function login_check(string $submitted_username): string|bool

## Description

Validates the submitted username and password for login authentication against existing usernames and hashed passwords stored in the 'trongate_administrators' table.


This method is designed to be invoked as a form validation callback.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $submitted_username | string | The username submitted for login authentication. | N/A | Required |

## Return Value


| Type | Description |
| ---|---|
| string\|bool | Returns TRUE (bool) if authentication is successful, otherwise returns an error message (string). |

## Example Usage

```php
if ($submit == 'Login') {
    $submitted_username = post('username');
    // Validate username and password for login.
    $this->validation->set_rules('username', 'username', 'required|callback_login_check');
    $this->validation->set_rules('password', 'password', 'required|min_length[5]');
    $result = $this->validation->run();

    if ($result === true) {
        $this->log_user_in($submitted_username);
    } else {
        // Reload login form on validation failure.
        $this->login();
    }
}
```
