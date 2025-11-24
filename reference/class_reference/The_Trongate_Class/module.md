# module()


protected function module(string $target_module): void

## Description

Loads a module using the Modules class. This method serves as an alternative way of invoking the load method from the Modules class. It simply instantiates a Modules object and calls its load method with the provided target module name.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $target_module | string | The name of the target module. | N/A |

## Return Value


| Type | Description |
| ---|---|
| void | This function does not return a value. |

## Example Usage

```php
$target_module = "my_module";
$this->module($target_module);
```
