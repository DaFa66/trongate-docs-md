# Additional Includes


HTML templates often need to load different JavaScript or CSS files depending on the specific page being rendered. Trongate provides a flexible system for handling these additional includes through the `_build_additional_includes()` method in the [Templates class](https://github.com/trongate/trongate-framework/blob/master/templates/controllers/Templates.php).

## Understanding Additional Includes


Additional includes allow you to dynamically add CSS and JavaScript files to your templates. These includes can be placed either in the header (top) or footer (bottom) of your HTML document.

### Basic Structure


The Templates class processes additional includes using two key variables:


- `$additional_includes_top`: For files that need to be included in the document head
- `$additional_includes_btm`: For files that need to be included at the bottom of the body

## Implementation in Templates


Here's how to implement additional includes in your template method:

```php
function admin(array $data): void {
    $data['additional_includes_top'] = $this->_build_additional_includes($data['additional_includes_top'] ?? []);
    $data['additional_includes_btm'] = $this->_build_additional_includes($data['additional_includes_btm'] ?? []);
    load('admin', $data);
}
```

### Template Usage


In your template file (e.g., `admin.php`), you can place the includes variables where you want the files to be loaded:

```vf
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <base href="<?= BASE_URL ?>">
    <link rel="stylesheet" href="css/trongate.css">
    <?= $additional_includes_top ?>
    <title>Admin</title>
</head>
<body>
    <!-- Your content here -->
    
    <script src="js/admin.js"></script>
    <?= $additional_includes_btm ?>
</body>
</html>
```

## Adding Files from Controllers


To add additional files from your controllers, pass them in the `$data` array:

```php
class Dashboard extends Trongate {
    
    function index() {
        $data['view_file'] = 'dashboard_view';
        $data['additional_includes_top'] = [
            'css/dashboard.css',
            'css/custom_charts.css'
        ];
        
        $data['additional_includes_btm'] = [
            'js/dashboard_charts.js',
            'js/dashboard_widgets.js'
        ];
        
        $this->template('admin', $data);
    }
}
```

## How It Works


The _build_additional_includes() method processes the files based on their extension:


- For `.js` files: Generates `<script src="..."></script>` tags
- For `.css` files: Generates `<link rel="stylesheet" href="...">` tags
- For other file types: Includes the file path as-is


The method also maintains proper HTML formatting by:


- Adding appropriate indentation
- Handling newlines for clean source code
- Ensuring proper closing of HTML tags

> [!TIP]
> **Best Practices**
>
> When working with additional includes, consider the following best practices:
> 
> ### 1. Group Your Includes Logically
> 
> 
> Organize your includes based on their purpose and loading requirements:
> 
> ```php
> $data['additional_includes_top'] = [
>     'css/custom/styles.css',
>     'third_party/plugin/plugin.css'
> ];
> 
> $data['additional_includes_btm'] = [
>     'js/custom_scripts.js',
>     'js/plugins.js'
> ];
> ```
> 
> ### 2. Use Conditional Loading
> 
> 
> Load files only when they're needed for specific functionality:
> 
> ```php
> if ($need_charts) {
>     $data['additional_includes_btm'][] = 'js/charts.js';
> }
> ```


> [!NOTE]
> **Just To Let You Know...**
>
> Remember to verify that all file paths are correct relative to your application's base URL. Incorrect paths may result in resources failing to load properly.


