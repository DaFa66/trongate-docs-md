# Introducing Themes


While templates provide a way to structure individual pages, Trongate's theming system offers a more comprehensive approach to managing your application's appearance. Themes allow you to package templates together with assets such as; stylesheets, fonts, images and JavaScript files to create cohesive design packages.

## Beyond Templates


A template is essentially an HTML file with embedded PHP code that defines a page's structure. However, modern web applications often require more sophisticated styling solutions that go beyond simple HTML templates. You might need:


- Multiple coordinated color schemes
- Custom typography and fonts
- Comprehensive icon sets
- Standardized UI components
- JavaScript enhancements
- Theme-specific assets and images


This is where Trongate's theming system comes into play, providing a structured way to manage all these design elements.

## Theme Architecture


In Trongate, a theme is more than just a collection of templates - it's a complete design package. Themes are defined in the [themes.php](https://github.com/trongate/trongate-framework/blob/master/config/themes.php) configuration file and are structured to provide flexible, reusable design systems.

### The Default Admin Theme


Trongate ships with a built-in 'admin' theme, which serves as an excellent example of the theming system's capabilities. This theme is implemented through the `admin()` method in the Templates class:

```php
/**
 * Loads the 'admin' view with provided data and additional includes.
 *
 * @param array $data Data array to be passed to the view.
 * @return void
 */
function admin(array $data): void {
    $data['additional_includes_top'] = $this->_build_additional_includes($data['additional_includes_top'] ?? []);
    $data['additional_includes_btm'] = $this->_build_additional_includes($data['additional_includes_btm'] ?? []);
    load('admin', $data);
}
```


While this method appears similar to standard template loading, it actually triggers Trongate's theme loading mechanism, pulling resources from the [themes](https://github.com/trongate/trongate-framework/tree/master/public/themes/) directory rather than the standard [templates directory](https://github.com/trongate/trongate-framework/tree/master/templates).

## Theme Configuration


Themes are defined in `config/themes.php`. Here's how the admin theme is configured:

```php
$admin_theme = [
    "dir" => "default_admin/blue",
    "template" => "admin.php",
];

$themes['admin'] = $admin_theme;
```


The configuration specifies:


- `dir`: The theme's directory path relative to the [themes](https://github.com/trongate/trongate-framework/tree/master/public/themes/) directory
- `template`: The [primary template file](https://github.com/trongate/trongate-framework/blob/master/public/themes/default_admin/blue/admin.php) for the theme

### Color Scheme Management


The admin theme demonstrates one of Trongate's powerful theming features: easy color scheme switching. By modifying the `dir` path from `default_admin/blue` to `default_admin/red`, you can instantly switch the entire admin interface to a different color scheme.

> [!NOTE]
> **Just To Let You Know...**
>
> Color schemes in Trongate themes are complete packages that include coordinated colors for all UI elements, ensuring consistency across your application.


## Theme Structure


A typical Trongate theme directory contains:


- Template files (`.php`)
- Stylesheets (`.css`)
- JavaScript files (`.js`)
- Theme-specific assets (images, fonts, icons)
- Color scheme variations


This structured approach allows themes to provide comprehensive design solutions while maintaining clean separation between different visual aspects of your application.

> [!TIP]
> **Best Practices**
>
> The next section will explore theme loading mechanics and how to create custom themes for your Trongate applications.


