# Creating Custom Themes


Trongate's theming system allows you to create comprehensive design packages that include templates, stylesheets, JavaScript files, and other assets. This guide will walk you through the process of creating your own custom theme.

## Theme Location


Themes in Trongate are stored in the `public/themes` directory of your application. Each theme gets its own subdirectory where all its resources are contained.

## Creating a Custom Theme

### Step 1: Plan Your Theme Structure


Before creating your theme, plan its structure and organization. Consider what elements your theme needs:


- Template files (`.php`)
- Stylesheets (`.css`)
- JavaScript files (`.js`)
- Images and icons
- Other assets (if needed)

### Step 2: Create the Theme Directory


Create a new directory in `public/themes` for your theme. Choose a descriptive name that reflects its purpose. For example:

```
public/themes/
    └── modern_dashboard/
        ├── default/
        │   ├── css/
        │   │   ├── style.css
        │   │   └── components.css
        │   ├── js/
        │   │   └── theme.js
        │   ├── images/
        │   │   └── logo.png
        │   └── dashboard.php
        └── css/
            └── shared.css
```

### Step 3: Create the Template File


Create your main template file (e.g., `dashboard.php`) in your theme directory:

```vf
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <base href="<?= BASE_URL ?>">
    
    <?php
    // Get root theme directory for shared assets
    $trimmed_theme_dir = rtrim(THEME_DIR, '/');
    $root_theme_dir = dirname($trimmed_theme_dir) . '/';
    ?>
    
    <!-- Core and shared styles -->
    <link rel="stylesheet" href="css/trongate.css">
    <link rel="stylesheet" href="<?= $root_theme_dir ?>css/shared.css">
    
    <!-- Theme-specific styles -->
    <link rel="stylesheet" href="<?= THEME_DIR ?>css/style.css">
    <link rel="stylesheet" href="<?= THEME_DIR ?>css/components.css">
    
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
    
    <!-- Theme JavaScript -->
    <script src="<?= THEME_DIR ?>js/theme.js"></script>
    <?= $additional_includes_btm ?? '' ?>
</body>
</html>
```

### Step 4: Register Your Theme


Open `config/themes.php` and add your theme configuration:

```php
$modern_dashboard = [
    "dir" => "modern_dashboard/default",
    "template" => "dashboard.php",
];

$themes['modern_dashboard'] = $modern_dashboard;

// If adding color variations
$modern_dashboard_dark = [
    "dir" => "modern_dashboard/dark",
    "template" => "dashboard.php",
];

$themes['modern_dashboard_dark'] = $modern_dashboard_dark;
```

## Key Theme Components


Your theme should include:


- A well-organized directory structure for assets
- The `base` tag with `BASE_URL` for proper path resolution
- Proper use of `THEME_DIR` for asset references
- The `Template::display($data)` call for content injection
- Support for additional includes (`$additional_includes_top` and `$additional_includes_btm`)

> [!NOTE]
> **Just To Let You Know...**
>
> When creating shared assets, consider placing them in a common directory at the theme root level. This allows multiple variations of your theme to access the same base resources while maintaining their unique styles.


## Using Your Theme


To use your new theme from any controller, specify it when calling the template method:

```php
class Dashboard extends Trongate {
    
    function index() {
        $data['view_file'] = 'dashboard_view';
        $data['template_title'] = 'Modern Dashboard';
        $this->template('modern_dashboard', $data);
    }
}
```

## Creating Theme Variations


To create variations of your theme (e.g., different color schemes):


1. Create a new directory within your theme folder for each variation
2. Include variation-specific assets (CSS, images, etc.)
3. Register each variation in `themes.php`
4. Keep shared assets in a common location

> [!TIP]
> **Best Practices**
>
> Always use unique, descriptive names for your themes to avoid conflicts with existing themes in the application or third-party theme packages.
> 
> 
> By properly structuring your theme and its variations, you create a maintainable and portable design package that can be easily shared across projects or with the community.


