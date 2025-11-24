# Creating Custom Templates


Trongate allows you to create custom HTML templates to define the structure and layout of your web pages. This guide will walk you through the process of creating your own template.

## Template Location


Templates in Trongate are stored within the 'templates' module, which is located in your application's root directory. This module follows the standard Trongate module structure, containing both 'controllers' and 'views' directories.

## Creating a Custom Template

### Step 1: Define Your Template Name


Choose a meaningful name for your template that reflects its purpose. Template names should be in snake_case format and clearly indicate the template's intended use. Some examples of good template names include:


- public_template
- admin_dashboard
- member_portal
- auth_pages
- sales_backend

### Step 2: Create the Template Method


Open the Templates.php controller file in your templates/controllers directory and add a new method for your template:

```php
class Templates extends Trongate {

    function custom_template(array $data): void {
        $data['additional_includes_top'] = $this->_build_additional_includes($data['additional_includes_top'] ?? []);
        $data['additional_includes_btm'] = $this->_build_additional_includes($data['additional_includes_btm'] ?? []);
        load('custom_template', $data);
    }

}
```

### Step 3: Create the Template View


Create a new PHP file in your templates/views directory with the same name as your template method. For example, if your method is named 'custom_template', create custom_template.php:

```vf
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <base href="<?= BASE_URL ?>">
    <link rel="stylesheet" href="css/trongate.css">
    <?= $additional_includes_top ?? '' ?>
    <title><?= $template_title ?? WEBSITE_NAME ?></title>
</head>
<body>
    <header>
        <nav>
            <!-- Your navigation content -->
        </nav>
    </header>

    <main>
        <?= Template::display($data) ?>
    </main>

    <footer>
        <!-- Your footer content -->
    </footer>

    <?= $additional_includes_btm ?? '' ?>
</body>
</html>
```

## Key Template Components


Your template should include several important elements:


- The `base` tag with `BASE_URL` for proper path resolution
- Core stylesheet includes for your application
- The `Template::display($data)` call where page content will be injected
- Placeholders for additional includes (`$additional_includes_top` and `$additional_includes_btm`)

> [!NOTE]
> **Just To Let You Know...**
>
> When creating a new template, ensure it's properly integrated with Trongate's core features by including the base href tag and Template::display() method. This ensures your template works seamlessly with the framework's routing and view management systems.


## Using Your Template


To use your new template from any controller, specify it when calling the template method:

```php
class Welcome extends Trongate {
    
    function index() {
        $data['view_file'] = 'welcome';
        $data['template_title'] = 'Welcome Page';
        $this->template('custom_template', $data);
    }

}
```

> [!WARNING]
> **Warning!**
>
> Always ensure your template name is unique within the Templates class to avoid conflicts with existing templates like 'admin' or 'public'.


