# login()


public function login(): void

## Description

Renders a login page for administrators.
## Accessing The Login Page


The default administration login page is accessible by navigating to a Trongate application's base URL followed by **tg-admin**. However, this URL can be customized to a preferred secret login URL by adjusting the 'Trongate_administrators.php' class.


To set a secret login URL, uncomment the line:

```
// private $secret_login_segment = 'tg-admin';
```


Subsequently, update the **$secret_login_segment** variable with the desired URL segment to set an alternative login URL.

## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not take any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return any value. |

## Example Usage #1


The code below illustrates how to create a hyperlink that redirects users to the admin login page upon clicking.  The assumption, for this example, is that the code would be added inside a view file or an HTML template:

```
<?= anchor('tg-admin', 'Admin Login') ?>
```
## Example Usage #2


In this alternative example, a CSS class, named as 'button', is added to a **login** hyperlink.  This gives the hyperlink the appearance and behaviour of a button:

```
<?= anchor('tg-admin', 'Admin Login', array('class' => 'button')) ?>
```
