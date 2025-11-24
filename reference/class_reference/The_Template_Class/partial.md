# partial()


public static function partial(string $file_name, ?array $data = null): void

## Description

Loads and includes reusable view components (partials) from the global templates directory. This method is primarily used for including common UI elements that are shared across multiple pages or modules, such as headers, navigation bars, footers, and other reusable components.
## Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| file_name | string | The path to the partial file relative to templates/views/, without the .php extension.<br>                      <br>  <br><br>                    Example: "partials/header" for templates/views/partials/header.php | N/A | Yes |
| data | array\|null | An associative array of variables to be extracted and made available within the partial.<br>                      <br>  <br><br>                    Example: ['page_title' => 'Welcome', 'user' => $user_object] | null | No |

## Return Value


| Type | Description |
| ---|---|
| void | This method does not return a value. It outputs the content directly. |

## File Path Resolution


| Component | Description | Example |
| ---|---|---|
| Base Path | APPPATH . 'templates/views/' | /var/www/html/app/templates/views/ |
| File Name | Provided path + .php | partials/header.php |
| Full Path | Complete file path | /var/www/html/app/templates/views/partials/header.php |

## Common Use Cases

### 1. Header with Dynamic Title

**Template usage:**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <?= Template::partial('partials/head', [
        'page_title' => $page_title,
        'meta_description' => $meta_description
    ]) ?>
</head>
```


**Partial content (partials/head.php):**

```
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title><?= $page_title ?? 'Default Title' ?></title>
<meta name="description" content="<?= $meta_description ?? '' ?>">
<link rel="stylesheet" href="<?= BASE_URL ?>css/styles.css">
```
### 2. Navigation with User State

**Template usage:**

```
<?= Template::partial('partials/navigation', [
    'user_id' => $user_id,
    'is_admin' => $is_admin,
    'active_page' => 'dashboard'
]) ?>
```


**Partial content (partials/navigation.php):**

```php
<nav class="navbar">
    <div class="container">
        <a class="navbar-brand" href="<?= BASE_URL ?>">Site Name</a>
        <ul class="nav-links">
            <?php if (isset($user_id)): ?>
                <li><a href="<?= BASE_URL ?>dashboard" class="<?= $active_page === 'dashboard' ? 'active' : '' ?>">Dashboard</a></li>
                <?php if ($is_admin): ?>
                    <li><a href="<?= BASE_URL ?>admin">Admin Panel</a></li>
                <?php endif; ?>
                <li><a href="<?= BASE_URL ?>logout">Logout</a></li>
            <?php else: ?>
                <li><a href="<?= BASE_URL ?>login">Login</a></li>
            <?php endif; ?>
        </ul>
    </div>
</nav>
```
### 3. Reusable Form Components

**Template usage:**

```
<?= Template::partial('partials/forms/text_input', [
    'label' => 'Email Address',
    'name' => 'email',
    'value' => $email ?? '',
    'required' => true,
    'error' => $errors['email'] ?? null
]) ?>
```


**Partial content (partials/forms/text_input.php):**

```php
<div class="form-group <?= isset($error) ? 'has-error' : '' ?>">
    <label for="<?= $name ?>">
        <?= $label ?>
        <?php if ($required ?? false): ?>
            <span class="required">*</span>
        <?php endif; ?>
    </label>
    <input type="text" 
           name="<?= $name ?>" 
           id="<?= $name ?>" 
           value="<?= htmlspecialchars($value) ?>"
           <?= ($required ?? false) ? 'required' : '' ?>>
    <?php if (isset($error)): ?>
        <div class="error-message"><?= $error ?></div>
    <?php endif; ?>
</div>
```
## Dependencies


| Dependency | Description |
| ---|---|
| APPPATH | Constant defining the application root path |
| attempt_include() | Private method that handles file inclusion and data extraction |

## Error Handling


If the specified partial file does not exist, the script will terminate with an error message showing the attempted file path. This behavior is handled by the attempt_include() method.

> [!WARNING]
> **Warning!**
>
> ### Important Notes
> 
> 
> - Partial files must be located within the templates/views directory
> - All variables in the $data array become available as individual variables in the partial
> - File paths are case-sensitive on Unix-based systems
> - The .php extension is automatically added to the file name
> - For module-specific partials, use Template::display() instead
