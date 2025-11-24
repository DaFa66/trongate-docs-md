# get_last_segment()


function get_last_segment(): string

## Description

Retrieves the value of the last segment of the current URL. It extracts the last segment by utilizing the 'get_last_part' function, which splits the URL by '/' and returns the last element.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not accept any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| string | The last segment of the URL. |

## Example Usage

```
$invoice_ref = get_last_segment();
```
