# How Templates Work With Views


When working with templates in Trongate, it's important to understand how they work with view files, and how data is passed between templates and views. This section explains the mechanisms that templates use to locate, load and inject content from view files.

## How Templates Locate View Files


When you call the template() method, Trongate needs to determine which view file to load into the template. This process is governed by two key properties in your `$data` array:


- `view_module`: Tells the template which module contains the view file
- `view_file`: Specifies the name of the view file to load

### View File Resolution Process


Let's examine how a template locates a view file through a practical example. Consider this URL:

```
https://example.com/products/details/88
```


And the corresponding controller code:

```php
class Products extends Trongate {
  
  function details() {
    $data['view_module'] = 'inventory';
    $data['view_file'] = 'product_details';
    $this->template('default', $data);
  }

}
```


In this case:


- When the template is loaded, it looks for the view file based on `view_module`
- Since `view_module` is set to 'inventory', the template will look in that module's **views** directory
- The view file will be loaded from: `modules/inventory/views/product_details.php`

### Default View Module Resolution


If `view_module` is not specified in the `$data` array, the template will use the first URL segment to determine where to look for the view file. For example:

```php
class Products extends Trongate {
  
  function details() {
    $data['view_file'] = 'product_details';
    $this->template('default', $data);
  }

}
```


In this case, since the URL begins with 'products', the template will look for the view file at:

```
modules/products/views/product_details.php
```

> [!TIP]
> **Best Practices**
>
> It's recommended to always specify `view_module` explicitly in your `$data` array, even when it matches the URL segment. This makes your code more maintainable and allows for easier implementation of custom routing rules in the future.


## Data Passing Between Templates and Views


Templates in Trongate automatically make variables from the `$data` array available to both the template file and the loaded view file. This happens through an automatic extraction process.

### Example: Data Extraction

```php
class Welcome extends Trongate {

  function hello() {
    $data['first_name'] = 'John';
    $data['view_file'] = 'hello_view';
    $this->template('default', $data);
  }

}
```


The template system will make `first_name` available directly in both the template and view file:

```vf
<!-- Inside your view file -->
<p>Hello, <?= $first_name ?>!</p>
```


This automatic extraction removes the need for manually unpacking variables from the `$data` array, making your template and view files cleaner and more intuitive to work with.

> [!NOTE]
> **Just To Let You Know...**
>
> Even though `$data` arrays are automatically extracted, the original array remains available from within the view file or template.  This is particularly useful for debugging purposes.  For example, if you are working with a view file and you'd like a reminder of what variables have been passed into the view file, you could use Trongate's json() method, like so:
> 
> ```vf
> <?= json($data) ?>
> ```


## The Template Display Method


Within your template files, use the display() method to specify where the view content should be inserted.


The `display()` method is a [static method](https://www.w3schools.com/php/php_oop_static_methods.asp) that exists within Trongate's internal [Template class](../../reference/class_reference/The_Template_Class).  Within a template file, this can be invoked with the following line of code:

```vf
<?= Template::display($data) ?>
```


Below is an example of a template file that uses the  `display()` method to inject view file content into the page.

```vf
<!DOCTYPE html>
<html>
<head>
    <title>My Site</title>
</head>
<body>
    <header>
        <!-- Template header content -->
    </header>

    <main>
        <?= Template::display($data) ?>
    </main>

    <footer>
        <!-- Template footer content -->
    </footer>
</body>
</html>
```


The `Template::display()` method:


- Loads the appropriate view file based on `view_module` and `view_file`
- Makes all `$data` variables available to the view
- Injects the rendered view content into the template

> [!NOTE]
> **Just To Let You Know...**
>
> This approach to template and view integration allows for a clean separation between your page's structure (defined in templates) and its specific content (defined in views), while maintaining a simple and intuitive way to pass data to both.


