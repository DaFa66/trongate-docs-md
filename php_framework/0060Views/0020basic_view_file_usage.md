# Basic View File Usage


This section introduces fundamental concepts of view file management, using a basic installation of Trongate as a starting point.


Upon installation, Trongate automatically loads the default 'welcome' module and its associated controller. Below is the initial structure of the 'Welcome' controller:

```php
&lt;?php
class Welcome extends Trongate {

    /**
     * Renders the default 'welcome' webpage for public access.
     *
     * @return void
     */
    function index(): void {
        $data['view_module'] = 'welcome'; // Indicates the module containing the view file.
        $data['view_file'] = 'welcome'; // Specifies the base name of the target PHP view file.
        $this->template('public', $data); // Loads the 'welcome' view file within the public template.
    }
}
```


If the `index()` method is invoked, as specified by the 
    [default homepage routing configuration](documentation/display/php_framework/understanding-routing/homepage-routing), 
    it loads a template and passes a `$data` array containing a 'view_file' property.

## Implementing a Custom Method


To illustrate basic view file usage, we add a custom method to the 'Welcome' controller. Here's a simplified implementation of the 'greeting' method:

```php
function greeting() {
    $this->view("greeting");
}
```

### Introduction to the "View" Method


To load view files, Trongate utilizes an internal method named 
    view().


In the provided example, the `view()` 
    method is invoked with the argument 'greeting'. This triggers a search in the 'views' directory of the current module for a file named 'greeting.php'. 
    If found, the content of this file is rendered and displayed in the browser.

> [!WARNING]
> **Warning!**
>
> The view() method of Trongate accepts the name of the view file as an argument. 
>         It is essential to **exclude** the file extension, such as '.php', from this argument.



With the addition of the `greeting()` method, the 'Welcome' controller will be extended as follows:

```php
&lt;?php
class Welcome extends Trongate {

    /**
     * Renders the default 'welcome' webpage for public access.
     *
     * @return void
     */
    function index(): void {
        $data['view_module'] = 'welcome'; // Indicates the module containing the view file.
        $data['view_file'] = 'welcome'; // Specifies the base name of the target PHP view file.
        $this->template('public', $data); // Loads the 'welcome' view file within the public template.
    }

    function greeting() {
        $this->view("greeting");
    }
}
```

> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** The example method named '**greeting**' omits elements such as type hinting, return types, 
>         visibility modifiers (public, private, protected), and doc blocks for brevity. 
>         These are essential for production code to ensure clarity, type safety, and proper documentation. 
>         For additional information, please refer to the Trongate framework's 
>         [coding style guide](documentation/display/php_framework/basic-concepts/regarding-coding-style).


## Creating a Simple View File


After defining the method to load a view file, the next step is creating a new PHP file named 'greeting.php' 
    within the 'views' directory of the 'welcome' module. This file will contain basic HTML content for demonstration purposes. 
    For example:

```html
<h1>Hello</h1>
<p>It's nice to see you!</p>
```

## Rendering the View File


To render the view file in the browser, navigate to `BASE_URL/welcome/greeting`. 
    If the `greeting()` method and the corresponding 'greeting.php' view file are correctly implemented, 
    the browser will display output similar to the following:

![Screenshot demonstrating the rendering of a simple view file.](https://trongate.io/images/78/greetingPZK7.png)
        
*Screenshot demonstrating the rendering of a simple view file.*
## Conclusion


This example provides a foundational overview of using view files within the Trongate framework. 
    By adding the `greeting()` method to the 'Welcome' controller, we demonstrate how Trongate's 
    `view()` method loads HTML content from a view file. 
    Remember to specify the view file name without the '.php' extension to ensure proper functionality.

