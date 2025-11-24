# Loading Templates


In Trongate, templates are loaded from within controllers using the template method. This technique ensures that pages can follow a defined layout while having dynamic content to be inserted as needed.

### Basic Syntax


To load a template, use the template method within a controller:

```php
class Example extends Trongate {
  
  function index() {
    $data['view_file'] = 'example_view';
    $this->template('public', $data);
  }

}
```


In this example:


- The first parameter (`'public'`) specifies which method should be invoked from the [Templates class](https://github.com/trongate/trongate-framework/blob/master/templates/controllers/Templates.php)
- The second parameter (`$data`) is an optional associative array containing variables to be passed into the template

## How Templates Work


When you call `$this->template()`, Trongate looks for a corresponding method in the Templates class. Here's an example of how the Templates class is structured:

```php
<?php
class Templates extends Trongate {

    /**
     * Loads the 'public' view with provided data.
     *
     * @param mixed $data Data array to be passed to the view.
     * @return void
     */
    function public($data): void {
        load('public', $data);
    }
}
```


The load() method is responsible for:


- Loading the template file from the `templates/views/` directory
- Making the `$data` array variables available to the template
- Handling the rendering of the template content

> [!NOTE]
> **Just To Let You Know...**
>
> Trongate includes an internal class named [Template](documentation-ref/list_refs/class_reference/the-template-class) (singular), which will be discussed in more detail later in this chapter.  However, this is an entirely different class and the two should not be confused.
> 
> 
> To be clear, [Template](https://github.com/trongate/trongate-framework/blob/master/engine/Template.php) and [Templates](https://raw.githubusercontent.com/trongate/trongate-framework/refs/heads/master/templates/controllers/Templates.php) are two separate and distinct PHP classes within the Trongate framework.
> 
> 
> - The **Template** class is an internal class, within Trongate's 'engine' directory.  It is responsible for manages loading and displaying of content within HTML templates.
> - The **Templates** class is part of a 'templates' module that exists within the root directory.  It *contains* the templates that are to be used within a given Trongate application.


### Template File Structure


Template files are PHP files stored in the `templates/views/` directory.  Usually, most of the content within a template file will be HTML code.  However, one of the strengths of PHP is that it can be seamlessly integrated with HTML.  Therefore, it's normal for template files to also contain *some* PHP code, as well as HTML.  Here's an example of a template file (named as '**public.php**'):

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <base href="<?= BASE_URL ?>">
    <link rel="stylesheet" href="css/trongate.css">
    <link rel="stylesheet" href="css/app.css">
    <title>My Application</title>
</head>
<body>
    <header>
        <div class="logo">
            <?= anchor(BASE_URL, WEBSITE_NAME) ?>
        </div>
        <nav>
            <ul>
                <li><?= anchor(BASE_URL, 'Home') ?></li>
                <li><?= anchor('about', 'About') ?></li>
                <li><?= anchor('contact', 'Contact') ?></li>
            </ul>
        </nav>
    </header>

    <main class="container">
        <?= Template::display($data) ?>
    </main>

    <footer>
        <div class="container">
            <div>&copy; <?= date('Y') . ' ' . OUR_NAME ?></div>
        </div>
    </footer>
</body>
</html>
```


Key points about the template file:


- The template provides the overall HTML structure for your pages
- `Template::display($data)` is where your view content will be injected
- Template files have access to framework constants like `BASE_URL` and helper functions like anchor()

## Dynamic Template Selection


Trongate allows templates to be dynamically switched at runtime based on context. For example, different templates can be loaded depending on a user's authentication status or access level.

### Example: Loading a Template Based on User Level

```php
class Dashboard extends Trongate {

  function index() {
    // Attempt to fetch the visitor's user level
    $this->module('trongate_tokens');
    $user_level = $this->trongate_tokens->_get_user_level();

    if ($user_level === false) {
        // User not logged in - redirect to login page
        redirect('login');
    }

    $template_to_use = ($user_level === 'admin') ? 'admin' : 'members_area';
    
    $data['view_file'] = 'dashboard_view';
    $this->template($template_to_use, $data);
  }

}
```


In this case:


- Admins see the template defined in `admin()` method of the Templates class
- Other authenticated users see the template defined in `members_area()` method
- Non-authenticated users are redirected to the login page

> [!NOTE]
> **Just To Let You Know...**
>
> Templates provide the structural foundation of your pages, while views contain the specific content that gets injected into these templates.
> 
> 
> The relationshp between templates and views is explored in the next section.


