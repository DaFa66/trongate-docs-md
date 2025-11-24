# submit_login()


public function submit_login(): void

## Description

Handles the submission of login forms, validating user input and logging users in if validation passes. Redirects to the login form on validation failure or to the base URL on 'Cancel' submission.
## Changing The Login Destination


To change the destination users are sent to upon successful login, modify the **$dashboard_home** variable at the top of the **Trongate_administrators** class. By default, it is set to **'trongate_pages/manage'**. For example:

```
// Where to redirect after successful login.
private $dashboard_home = 'custom_path/dashboard';
```

## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not take any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return any value. |

## Example Usage

```
// Example Usage not available for this method
```
