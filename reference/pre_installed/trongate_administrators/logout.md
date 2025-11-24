# logout()


public function logout(): void

## Description

Handles user logout by destroying tokens and redirects based on the existence of the secret login segment.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not take any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return any value. |

## Example Usage


The code below illustrates how to create a hyperlink that triggers the **logout()** method upon clicking:

```
<?= anchor('trongate_administrators/logout', 'Log Out') ?>
```
