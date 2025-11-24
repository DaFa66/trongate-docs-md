# get_num_segments()


function get_num_segments(): int

## Description

Retrieves the number of segments in the current URL after the base URL. It calculates the number of segments by removing the base URL and then splitting the remaining path into segments using '/' as the delimiter.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not accept any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| int | The number of URL segments after the base URL. |

## Example Usage

```
$num_url_segments = get_num_segments();
```
