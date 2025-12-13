# The Structure of a Controller


Within the Trongate framework, controllers are PHP classes that extend the built-in [Trongate class](documentation-ref/list_refs/class_reference/the-trongate-class). Extending this foundational class provides controllers with immediate access to all of Trongate's core functionalities, such as form validation, database interactions, URL helpers, and more, enabling them to efficiently manage application logic and user interactions.

## Naming Conventions


It is crucial to adhere to the following naming conventions when working with Trongate controllers:


1. **File Naming:** Controller file names should start with a capital letter, reflecting their importance and usage within the module.
2. **Class Naming:** Similarly, controller class names should begin with a capital letter, aligning with PHP's best practices for class definitions.
3. **Module Naming:** The controller class name should correspond to the name of its module, which can be in all lowercase. This consistency aids in maintaining a clear and logical structure within the project.

## Example: The Dice Controller


Below is an example of a simple Trongate controller file named 'Dice.php', located within a hypothetical module named 'dice'. This example demonstrates how a controller can encapsulate specific functionalities:

```php
<?php
class Dice extends Trongate {

    function roll() {
        $number = rand(1, 6);
        echo $number;
    }
    
}
```

## Detailed Breakdown of the Dice Controller


The 'Dice' controller provides a demonstration of how controllers are structured and function within the Trongate framework. Let's examine each component of the controller:

### PHP Opening Tag

```php
<?php
```


This is the opening tag for any PHP script. It tells the server that the code following this tag should be interpreted as PHP code.

### Class Declaration

```php
class Dice extends Trongate {
```


This line declares a new class named 'Dice' which extends the 'Trongate' class. Extending a class in PHP is a fundamental aspect of object-oriented programming that allows the 'Dice' class to inherit all methods and properties of the Trongate framework's base class.

### Function Declaration

```php
function roll() {
```


The code above is the first line of a method named 'roll' within the Dice class. Methods are functions that are defined inside a class and describe the behaviors or capabilities of objects created from the class. In Trongate, as in many MVC frameworks, these methods can be linked to specific routes (URLs).

> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** For brevity, the example provided omits elements such as type hinting, return types, visibility modifiers (public, private, protected), and doc blocks. These are essential for production code to ensure clarity, type safety, and proper documentation. For additional information on this topic, please refer to the Trongate framework's [coding style guide](../0030Basic_Concepts/0010regarding_coding_style.md).


### Method Functionality


Within the curly braces of the `roll()` method, we have this line of code:

```php
$number = rand(1, 6);
```


The above line of code generates random number between 1 and 6 and assigns to the variable, `$number`.

> [!NOTE]
> **Just To Let You Know...**
>
> The `rand()` function is a built-in PHP function used to generate random numbers.



Moving on, the next line of code - within the `roll()` method is as follows:

```php
echo $number;
```


This line outputs the value of `$number` to the webpage. In the context of a controller within a framework like Trongate, this typically means sending the data back to the client's browser where it can be rendered as part of the HTML or handled via JavaScript.

### Class and Method Closure


Finally, the `roll()` method is closed with a closing curly bracket:

```php
}
```

> [!NOTE]
> **Just To Let You Know...**
>
> In PHP, as in many other programming languages, curly braces are used to define the scope of classes, methods, and other control structures, ensuring that the code enclosed within them is associated with that specific class or method.



This breakdown highlights how the 'Dice' controller leverages both [Trongate's](documentation/reference) and PHP's built-in functionalities to perform its tasks, generating a random number between one and six.

## Accessing the Controller


The `roll()` method can be invoked by navigating to the following URL:

`http://example.com/dice/roll`
This URL structure would cause the 'roll' method to be invoked, generating a random number between one and six using PHP's inbuilt rand() function. The random number that has been generated would then be displayed on the screen.

![Sample output](https://trongate.io/images/73/roll_theZzyt.png)
        
*Sample browser output (zoomed in for clarity)*
## URL Mapping and Routing


The URL provided adheres to Trongate's [rules for automatic URL routing](../0040Understanding_Routing/0020automatic_url_routing.md). In the example above:


- The first URL segment, `dice`, maps to a class named 'Dice'. This class is part of a module also named 'dice'.
- The second URL segment, `roll`, specifies the method to be invoked. Thus, it triggers the `roll()` method within the loaded Dice class.


This structured URL pattern ensures that requests are routed efficiently to the appropriate controller actions, making URL management straightforward and intuitive within the Trongate framework.

