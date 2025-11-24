# explorer()


function explorer(): void

## Description

Renders the API explorer interface for development purposes. This method provides a user interface for exploring and testing API endpoints during development. If the application is not in 'dev' mode, the API explorer will be disabled with a 403 Forbidden response. The method attempts to identify the target database table by reading the third segment of the URL. If a table with a name matching the third URL segment is not found in the database, a 404 Not Found response will be returned.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not take any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return anything directly, but it outputs HTML content for the API explorer. |

## Example Usage

```
To load the API Explorer, navigate to the BASE_URL followed by 
api/explorer/[target_table_name].
```
