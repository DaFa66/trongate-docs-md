# run()


function run(string $module_controller_method, mixed $first_value = null, mixed $second_value = null, mixed $third_value = null): mixed

## Description

Dynamically invokes module's controller method and is specifically designed to be called from within presentation files, such as view files.
## Parameters


| Parameter | Type | Description | Default |
| ---|---|---|---|
| $module_controller_method | string | The format is "Module/Controller/Method". | N/A |
| $first_value | mixed | Optional. First parameter for the method. | null |
| $second_value | mixed | Optional. Second parameter for the method. | null |
| $third_value | mixed | Optional. Third parameter for the method. | null |

## Return Value


| Type | Description |
| ---|---|
| mixed | The result of the controller method. |

## Example Usage

```
<?= Modules::run('Accounts/_display_profit', $data) ?>
```
