# get_view_module()


public static function get_view_module(): string

## Description

Extracts and processes the view module name from the current URL. This method removes the base URL, sanitizes the remaining path, and returns the first URL segment as the view module name. If no segment is found, it returns a default module value.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| This method does not accept any parameters. |  |  |  |  |

## Return Value


| Type | Description |
| ---|---|
| string | The name of the view module extracted from the URL. If no module is found in the URL, returns the value of DEFAULT_MODULE constant. |

## Dependencies


| Dependency | Description |
| ---|---|
| BASE_URL | Constant defining the base URL of the application |
| DEFAULT_MODULE | Constant defining the fallback module name |
| current_url() | Function that returns the current URL |

## Example Usage

```
// Assuming current URL is: http://example.com/admin/dashboard
$view_module = Template::get_view_module(); // Returns 'admin'

// Assuming current URL is: http://example.com/user-profile
$view_module = Template::get_view_module(); // Returns 'user/profile'

// Assuming current URL is: http://example.com/
$view_module = Template::get_view_module(); // Returns value of DEFAULT_MODULE
```
