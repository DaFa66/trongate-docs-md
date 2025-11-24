# reset()


function reset(): void

## Description

Restores the 'default' homepage content. This method checks the environment and responds with an HTTP 403 Forbidden status if it's not in 'dev' mode. It then determines whether to create a new homepage record or update the existing one based on the number of records in the 'trongate_pages' table.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not accept any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| void | Returns nothing. |

## Example Usage

```php
$this->module('trongate_pages');
$this->trongate_pages->reset();
```
