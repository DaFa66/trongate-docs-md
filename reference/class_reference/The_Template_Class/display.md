# display()


public static function display(?array $data = null): void


**Note:** This method accepts only one argument - an optional array parameter. Multiple arguments are not supported.

## Description

Core template rendering method that loads and displays view files from module directories.  This method should be invoked from within a view file or an HTML template.


This method serves two primary purposes:


- Rendering the main content area within a template
- Including module-specific partial views when Template::partial() is insufficient


The method automatically determines the correct module and view file to load based on the URL structure, but these can be overridden through the $data array.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| data | array\|null | An associative array that can contain:<br><br>- `view_module`: The module directory name<br>- `view_file`: The view file name (without .php extension)<br>- Any additional variables needed by the view | null | No |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return a value. It outputs the content directly. |

## File Path Resolution


| Component | Source | Example |
| ---|---|---|
| view_module | First URL segment or $data['view_module'] | shop |
| view_file | $data['view_file'] or 'index' | product_list |
| Final Path | APPPATH/modules/[module]/views/[file].php | APPPATH/modules/shop/views/product_list.php |

## Common Use Cases

### 1. Main Content Area

Using display() to render the main content in a template:

```
<!DOCTYPE html>
<html>
    <head>
        <title>My Site</title>
    </head>
    <body>
        <header>...</header>
        <main>
            <?= Template::display($data) ?>
        </main>
        <footer>...</footer>
    </body>
</html>
```
### 2. Module-Specific Partials

Loading a partial view from a specific module:

```
// Inside a controller or view
$data = [
    'view_module' => 'shop',
    'view_file' => 'product_sidebar',
    'categories' => $categories,
    'featured_products' => $featured_products
];
Template::display($data);
```
### 3. Default Index Page

When no view_file is specified, it loads index.php:

```
// These are equivalent:
Template::display();
Template::display(['view_file' => 'index']);
```
## Dependencies


| Dependency | Description |
| ---|---|
| APPPATH | Constant defining the application root path |
| get_view_module() | Method that retrieves the current view module from the URL |
| attempt_include() | Private method that handles file inclusion and data extraction |

## Error Handling


If the specified view file does not exist, the script will terminate with an error message showing the attempted file path. This behavior is handled by the attempt_include() method.

> [!WARNING]
> ### Important Notes
> 
> 
> - All variables in the $data array become available as individual variables in the view file
> - The view_module and view_file values in $data override the URL-based defaults
> - View files must have a .php extension (added automatically)
> - File paths are constructed using directory separators appropriate for the operating system
