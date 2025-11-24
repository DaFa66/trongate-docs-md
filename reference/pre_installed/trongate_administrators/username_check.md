# username_check()


public function username_check(string $str): string|bool

## Description

Checks the availability of a username and validates it against existing usernames in the 'trongate_administrators' table.


This method is designed to be invoked as a form validation callback.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| $str | string | The username to be checked. | N/A | Required |

## Return Value


| Type | Description |
| ---|---|
| string\|bool | Returns an error message (string) if the username is not available, otherwise returns TRUE (bool). |

## Example Usage

```php
$submit = post('submit');

if ($submit == 'Submit') {
    // Set validation rules for username, password, and repeat password.
    $this->validation->set_rules('username', 'username', 'required|min_length[5]|callback_username_check');
    $this->validation->set_rules('password', 'password', 'required|min_length[5]');
    $this->validation->set_rules('repeat_password', 'repeat password', 'matches[password]');

    $result = $this->validation->run();

    if ($result == true) {
        // Form validation success.
        echo 'Success!';
    } else {
        // Form validation error(s);
        echo validation_errors('<div class="error-message">', '</div>');
    }
}
```
