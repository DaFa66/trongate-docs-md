# Multiple Classes Within One Module


Typically, the 'controllers' directory within a given module will contain one PHP file. This file generally defines a single PHP class, named after the module itself, but with the first letter capitalized in both the filename and the class name to adhere to PHP naming conventions.


This section explores scenarios where a module's 'controllers' directory contains more than one PHP class, detailing the considerations and best practices for organizing multiple classes within a single 'controllers' directory.

> [!WARNING]
> **Warning!**
>
> This page addresses a hypothetical edge case where it might be desirable to have multiple controller files within a single 'controllers' sub-directory.
> 
> 
> Under normal operational conditions, however, it is generally preferable to separate PHP classes into distinct modules, adhering to a '**one class per module**' structure. It's worth noting that Trongate supports modular nesting, which allows the inclusion of modules within modules. This approach offers a more scalable and organized alternative compared to the methods described here. For more information, see the following chapter: [Modules Within Modules](documentation/display/php_framework/parent-and-child-modules).


## Step 1: Creating an Additional PHP Class


To add a second PHP class within the 'controllers' directory of a Trongate module, create a new PHP file alongside your primary controller. The file name should clearly reflect its purpose, starting with a capital letter in accordance with PHP class naming conventions.


**Example:** Suppose you want to add a class named 'Greeting' within the 'controllers' directory of Trongate's default 'Welcome' module. The first step is to create a file named 'Greeting.php'. This file should be placed inside the 'controllers' directory of the 'welcome' module.


For demonstration purposes, the PHP class named 'Greeting' may be defined as follows:

```php
<?php
class Greeting {

    // Return a friendly greeting.
    function get_greeting($name) {
        $greeting = 'Hello '.$name.'. It\'s nice to see you!';
        return $greeting;
    }

}
```

> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** The example provided omits elements such as type hinting, return types, visibility modifiers (public, private, protected), and doc blocks for brevity. These are essential for production code to ensure clarity, type safety, and proper documentation. For additional information, please refer to the Trongate framework's [Coding Style Guide](documentation/display/php_framework/basic-concepts/regarding-coding-style).



This class provides a simple method to return a greeting message. By placing this class in the 'controllers' directory, it is organized alongside other related controllers, ensuring that your module remains tidy and manageable.

## Step 2: Loading the Additional PHP Class


Once you have created an additional PHP class within the 'controllers' directory, the next step is to ensure that this class is properly loaded and accessible where needed. In Trongate, this typically involves using `require_once` or a similar include statement to ensure the class is available without causing redundancy or errors.


**Why Use `require_once`?** This PHP statement is crucial in situations where the same file might be included multiple times during a request. It ensures that the file is included only once, preventing errors and behavior anomalies that occur from multiple inclusions, such as redeclaration errors.

### Example of Loading an Additional Class


Consider that you have the `Greeting` class in a file named 'Greeting.php' within the 'welcome' module's 'controllers' directory. To use this class in your main controller or anywhere within the module, you would include it using the following PHP statement:

```php
<?php
require_once 'Greeting.php';

class Welcome extends Trongate {

    function test($name) {
        $greeting = new Greeting();
        $name = 'John';
        $message = $greeting->get_greeting($name);
        echo $message;
    }

}
```


This example demonstrates how to load the 'Greeting' class and use it within the 'Welcome' controller. The `require_once` statement is placed at the top of the file, ensuring that the 'Greeting' class is available to the 'Welcome' controller methods.

### Best Practices for Loading Additional Classes


- **Location of Include Statements:** Place all include statements at the beginning of the file. This practice makes it easier to track which dependencies are used in the file and prevents issues related to undeclared classes.
- **Avoid Overloading:** Only include classes that are necessary for the functionality of the current PHP file. Overloading a file with unnecessary includes can lead to performance issues and complicates debugging.
- **Consider Use of Additional Modules:** For larger projects, consider creating additional modules or child modules for situations where multiple PHP classes need to be called from a module.


By following these guidelines, you can efficiently manage and utilize multiple classes within your Trongate module, ensuring that each class is loaded appropriately and is ready to fulfill its role within the application.

> [!NOTE]
> **Just To Let You Know...**
>
> **Controllers vs. Ordinary PHP Classes:** Not every PHP class within a 'controllers' directory qualifies as a 'controller' in the traditional sense. Typically, a controller is directly involved in handling HTTP requests, responding to user actions, managing the flow between the model and the view, and encapsulating the business logic required for these interactions.
> 
> 
> The example provided on this page introduces the loading of a basic PHP class, rather than an additional controller. This distinction is important, and it should be noted that the example provided has been intentionally simplified to facilitate understanding.


