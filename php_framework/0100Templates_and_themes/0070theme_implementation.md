# Theme Implementation


This section covers the practical aspects of working with themes in Trongate, including theme structure, asset management, and theme creation.

## Theme Location and Structure


Themes in Trongate are stored in the `public/themes/` directory. Within this directory, you have complete flexibility to structure your themes as needed for your application.

### Example: Admin Theme Structure


The default admin theme demonstrates one possible way to organize theme variations:

```
public/themes/default_admin/
    ├── Black/
    │   └── css/
    ├── Blue/
    │   └── css/
    ├── Green/
    │   └── css/
    ├── Orange/
    │   └── css/
    └── Purple/
        └── css/
```


Alternative structures are possible. For example, a theme with shared assets might use:

```
public/themes/new_admin/
    ├── css/
    ├── dark/
    │   ├── css/
    │   ├── js/
    │   └── admin.php
    └── light/
        ├── css/
        ├── js/
        └── admin.php
```

## Managing Theme Assets


Trongate provides the `THEME_DIR` constant for referencing theme-specific assets. This constant becomes available when a theme is loaded.

### Example: Loading Theme-Specific and Shared Assets

```vf
<!DOCTYPE html>
<html lang="en">
<head>
    <base href="<?= BASE_URL ?>">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <?php
    // Get the root theme directory for shared assets
    $trimmed_theme_dir = rtrim(THEME_DIR, '/');
    $root_theme_dir = dirname($trimmed_theme_dir) . '/';
    ?>
    
    <!-- Load shared CSS for all theme variations -->
    <link rel="stylesheet" href="<?= $root_theme_dir ?>css/adminroot.css">
    
    <!-- Load variation-specific CSS -->
    <link rel="stylesheet" href="<?= THEME_DIR ?>css/admintheme.css">
</head>
```


This approach allows you to:


- Share common assets across theme variations
- Override specific styles for each variation
- Maintain a clean separation between shared and variation-specific assets

## Registering Themes


Themes are registered in the `config/themes.php` file. Each theme requires two key properties:


- `dir`: The theme's directory path relative to `public/themes/`
- `template`: The primary template file for the theme

### Example: Theme Registration

```php
// Admin theme with color variation
$admin_theme = [
    "dir" => "default_admin/blue",
    "template" => "admin.php",
];
$themes['admin'] = $admin_theme;

// Desktop app theme
$desktop_app_mx = [
    "dir" => "desktop_app_mx/blue",
    "template" => "desktop_app_mx.php",
];
$themes['desktop_app_mx'] = $desktop_app_mx;

// Define themes constant
define('THEMES', $themes);
```

> [!NOTE]
> **Just To Let You Know...**
>
> Theme keys (e.g., 'admin', 'desktop_app_mx') should be unique and descriptive, as they'll be used to reference the theme in your application code.


## Theme Loading Process


When a theme is loaded via the template() method, Trongate:


1. Checks if the requested template exists in `THEMES`
2. If found, constructs the theme path using the theme's directory and template file
3. Defines `THEME_DIR` for asset referencing
4. Loads the template file with any provided data

> [!TIP]
> **Best Practices**
>
> - **Asset Organization:** Consider separating shared and variation-specific assets
> - **Theme Variations:** Use consistent directory structures across variations
> - **Asset References:** Always use `THEME_DIR` for theme-specific assets
> - **Theme Registration:** Use clear, descriptive keys in `themes.php`
> - **Directory Structure:** Choose a structure that makes sense for your specific needs - there's no mandatory layout


## The Benefits of Using Themes


While templates serve their purpose for basic page layouts, themes offer several significant advantages that make them invaluable for modern web applications:


- **Portability:** Entire design packages can be contained within a single folder, making them easy to transfer between projects or share with the community
- **Complete Design Systems:** Themes can include everything needed for a consistent look and feel:
        
- Templates
- Stylesheets
- JavaScript files
- Images and icons
- Fonts
- Color schemes


    
- **Easy Switching:** Change the entire appearance of your application by modifying a single line in your theme configuration
- **Version Control:** Keep entire design packages under version control as a single unit, making it easier to track design changes
- **Resource Management:** The `THEME_DIR` constant provides a reliable way to reference theme-specific assets, eliminating path management headaches
- **Multiple Variations:** Support different color schemes or design variations without duplicating your entire codebase
- **Clean Separation:** Keep design assets separate from your application logic, improving maintainability
- **Rapid Deployment:** Quick implementation of new designs by switching themes, perfect for A/B testing or seasonal changes


These benefits make themes particularly valuable for applications that require flexible styling, multiple design variations, or the ability to quickly change their appearance.

