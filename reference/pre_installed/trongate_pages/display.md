# display()


function display(): void

## Description

Attempts to display a page by reading a value from the URL.  If the last segment of the URL is 'edit' the method also verifies if the user is an admin so that permissions may be granted for editing. If no matching record is found in the 'trongate_pages' table, a 404 error page is displayed. Additionally, it ensures that only published pages are displayed unless the page is being edited.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not take any parameters, however, it does attempt to fetch a record from the 'trongate_pages' database table based on a value that is read from the URL. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return any value. |

## Example Usage

```
// Example Usage not available for this method
```
