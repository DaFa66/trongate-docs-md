# load()


function load(string $target_module): void

## Description

Loads a module by instantiating its controller.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $target_module | string | The name of the target module. | N/A |

## Return Value


| Type | Description |
| ---|---|
| void | No return value. |

## Example Usage

```php
$this->modules->load("welcome");
```
## Alternative Technique

The main Trongate class provides the `module()` method as a convenient alias to `$this->modules->load()`. This method offers a semantically clear alternative for developers, ensuring the codebase remains expressive and maintainable while utilizing the same underlying functionality as the `load()` method.

### Example Usage of Alternative Technique

```php
$this->module('welcome');
```
