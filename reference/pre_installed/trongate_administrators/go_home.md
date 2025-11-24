# go_home()


public function go_home(): void

## Description

Redirects to the designated dashboard home page.
## Customizing the Redirect URL


The default dashboard home URL is set to **trongate_pages/manage**. To change this destination, modify the **$dashboard_home** property at the top of the **Trongate_administrators** class in the PHP file.


To change the dashboard home URL, open Trongate_adminstrators.php and uncomment this line:

```
// private $dashboard_home = 'trongate_pages/manage';
```


Then, replace **'trongate_pages/manage'** with your preferred URL path.

## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not take any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return any value. |

## Example Usage #1


The code below demonstrates how to create a hyperlink that redirects users to the dashboard home page upon clicking:

```
<?= anchor('trongate_administrators/go_home', 'Dashboard Home') ?>
```
## Example Usage #2


In this alternative example, a CSS class named 'button' is added to the dashboard home hyperlink, giving it the appearance and behavior of a button:

```
<?= anchor('trongate_administrators/go_home', 'Dashboard Home', array('class' => 'button')) ?>
```
