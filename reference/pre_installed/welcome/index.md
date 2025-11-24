# index()


function index(): void

## Description

Renders the (default) homepage for public access. This method loads the 'trongate_pages' module and calls its 'display()' method to render the homepage.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not take any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return any value. |

## Example Usage #1


The code below shows the current implementation of the Welcome module's index method.

```php
/**
 * Renders the (default) homepage for public access.
 *
 * @return void
 */
public function index(): void {
  $this->module('trongate_pages');
  $this->trongate_pages->display();
}
```
## Example Usage #2


The code sample below demonstrates how to render a simple, 'hello world' message when the application's (default) homepage is loaded.

```php
/**
 * Renders the (default) homepage for public access.
 *
 * @return void
 */
public function index(): void {
  echo 'hello world';
}
```
## Example Usage #3


The code sample below demonstrates how a website template, with corresponding view file, could be rendered when the application's (default) homepage is loaded.

```php
/**
 * Renders the (default) homepage for public access.
 *
 * @return void
 */
public function index(): void {
  $data['view_module'] = 'welcome';
  $data['view_file'] = 'homepage_content';
  $this->template('public', $data);
}
```
