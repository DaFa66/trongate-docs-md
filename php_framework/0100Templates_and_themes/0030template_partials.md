# Template Partials


Partials are reusable pieces of code that represent specific sections of a web page. They allow developers to break down complex templates into smaller, more manageable components. Common examples of partials include:


- Headers
- Footers
- Navigation bars
- Sidebars
- Login forms


By using partials, you can maintain a consistent design across your application while reducing code duplication.

> [!NOTE]
> **Just To Let You Know...**
>
> The use of partials in templates is entirely **optional** and not required.
> 
> 
> While Trongate *does* support partials, this feature has been included primarily to accommodate developers who are accustomed to their use in other frameworks. We understand that transitioning to alternative methodologies can sometimes be challenging, but rest assured, there are other approaches that can be equally effective and more suited to modern development practices.
> 
> 
> For those seeking alternatives to partials, Trongate offers the option to [load entire modules directly from view files or templates](../0080Modules_Calling_Modules/0020loading_modules_from_views.md).


## How to Use Partials


In Trongate, partials are loaded using the partial() method. This method allows you to include a partial file from the `templates/views/` directory. Here's a basic example:

```vf
&lt;?= Template::partial("footer") ?&gt;
```


In this example, the `footer.php` file located in `templates/views/` will be included in the template.

### Passing Data to Partials


Partials can receive and display data passed from the calling module. You can pass data to a partial by including a `$data` array as the second argument:

```vf
&lt;?= Template::partial("footer", $data) ?&gt;
```


Inside the partial, all variables in the `$data` array are automatically extracted and can be accessed directly. For example, if `$data['year'] = 2023`, you can use `$year` inside the partial.


---

## Nested Partials


Partials can include other partials, allowing you to create complex, nested structures. For example, a `footer.php` partial might itself include a `social_links.php` partial:

```vf
&lt;footer&gt;
  &lt;p&gt;&copy; 2023 My Company&lt;/p&gt;
  &lt;?= Template::partial("social_links") ?&gt;
&lt;/footer&gt;
```


This nesting capability makes partials a powerful tool for building modular and reusable templates.

## Example: Template Without Partials


Here's an example of a template that does **not** use partials:

```vf
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
  &lt;title&gt;Document&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;header&gt;Acme Web Development Ltd&lt;/header&gt;
  &lt;main&gt;&lt;?= Template::display($data) ?&gt;&lt;/main&gt;
  &lt;footer&gt;&amp;copy; Copyright 2088 - All rights reserved&lt;/footer&gt;
&lt;/body&gt;
&lt;/html&gt;
```

## Example: Template With Partials


Here's the same template, but with the footer being loaded as a partial:

```vf
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt;
  &lt;title&gt;Document&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;header&gt;Acme Web Development Ltd&lt;/header&gt;
  &lt;main&gt;&lt;?= Template::display($data) ?&gt;&lt;/main&gt;
  &lt;?= Template::partial('footer', $data) ?&gt;
&lt;/body&gt;
&lt;/html&gt;
```

## Organizing Partials into Subdirectories


If you prefer to organize your partials into subdirectories (e.g., `templates/views/partials/`), you can do so by specifying the full path when calling `Template::partial()`. For example:

```vf
&lt;?= Template::partial("partials/footer") ?&gt;
```


This would look for `templates/views/partials/footer.php`.

## In Summary


Partials are a powerful feature in Trongate that allow you to break down your templates into reusable components. Whether you're building a simple website or a complex web application, partials can help you maintain a clean and organized codebase. By using `Template::partial()`, you can easily include global or module-specific partials, pass data to them, and even nest partials within each other.

