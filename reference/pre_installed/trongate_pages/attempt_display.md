# attempt_display()


function attempt_display(): void

## Description

Attempts to display a page by invoking the **display()** method of the Trongate Pages module. It is designed to be triggered automatically in instances where normal URL routing has failed to match a URL to a corresponding page and immediately before displaying a 404 (Not Found) page. This triggering behavior is governed by the INTERCEPT_404 constant, which is commonly configured within the config.php file of the Trongate framework.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not take any parameters, however, it delegates the task of displaying a page to the display() method of the Trongate Pages module. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return any value. |

## Example Usage

```
// Example Usage not available for this method
```
