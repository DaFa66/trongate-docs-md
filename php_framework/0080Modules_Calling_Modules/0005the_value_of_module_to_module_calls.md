# The Value of Module-to-Module Calls


Trongate is a robust and flexible PHP framework designed to facilitate efficient and maintainable web application development. One of its key features is the ability to load modules from other modules. This capability provides several significant benefits, enhancing both the architecture and functionality of your applications.

> [!NOTE]
> **Just To Let You Know...**
>
> Throughout this documentation, you will encounter the terms '**calling** module(s)', '**loading** module(s)', and '**invoking** module(s)'. These terms are used interchangeably and essentially mean the same thing: utilizing the functionality of one module within another module. This process involves making a module's methods and properties available in the context of another module to achieve a specific functionality or result.


## Benefits of Loading Modules from Other Modules

### Code Reusability


Loading modules from other modules promotes code reusability. By encapsulating specific functionality within modules, developers can easily reuse that functionality across different parts of the application without duplicating code. This leads to more efficient development processes and a reduction in potential errors.

### Separation of Concerns


Separation of concerns is a fundamental principle in software development. By keeping different functionalities in distinct modules, developers can ensure that each module handles a specific aspect of the application. This modular approach makes the codebase more organized, easier to understand, and simpler to maintain.

### Improved Maintainability


Maintaining a large codebase can be challenging. By dividing the application into modules, each handling a specific function, changes or updates can be made more easily. If a particular functionality needs to be modified, developers can focus on the relevant module without affecting other parts of the application.

### Enhanced Collaboration


In a collaborative development environment, different team members can work on different modules simultaneously. This modular structure facilitates parallel development, as changes in one module are less likely to interfere with the work being done on other modules. It also makes code reviews and testing more manageable.

### Scalability


As your application grows, the ability to load modules from other modules helps in scaling the application efficiently. New functionalities can be added as separate modules without disrupting the existing architecture. This modular approach ensures that the application remains scalable and manageable over time.

### Flexibility


Loading modules from other modules provides the flexibility to create complex and feature-rich applications. Developers can combine various modules to build sophisticated functionalities while keeping the codebase clean and maintainable. This flexibility allows for rapid development and easy integration of new features.

### Enhanced Performance


Trongate's module loading system offers significant performance advantages over the PSR-4 autoloading standard used in many PHP frameworks. Unlike PSR-4, which involves a round trip to a 'vendor' directory and introduces additional overhead, Trongate provides a more direct loading mechanism. This streamlined approach eliminates unnecessary processing steps, resulting in faster module retrieval and notably improved application performance.

## Conclusion


The ability to load modules from other modules is a powerful feature of the Trongate framework. It offers numerous benefits, including code reusability, separation of concerns, improved maintainability, enhanced collaboration, scalability, and flexibility. By leveraging this capability, developers can create robust, efficient, and maintainable web applications that are well-organized and easy to scale.

# Loading Modules From Controllers


Within the Trongate framework, there are two primary methods for a module to load another module.


The first method involves loading a module from within a *controller* file, while the second involves loading a module from a *view* file. This section focuses on loading a module from a controller file.


To load a module from a controller, use the following syntax:

```php
$this->module("module_name");
$this->module_name->do_something();
```


As illustrated, only two lines of code are required to load a method from a different module.


Below is an improved example demonstrating how to call a 'Tax' module to calculate the final price after tax has been applied. This method first loads the 'Tax' module and then invokes its method to add tax to the base price.

```php
function calculate_total_price($base_price) {

  // Load the "Tax" module
  $this->module("tax");

  // Calculate the final price by adding tax using the "Tax" module
  $final_price = $this->tax->add_tax($base_price);
  return $final_price;
}
```


Here is a more complex example that involves loading and using three different modules: 'Tax', 'Shipping', and 'Discount'. This method calculates the final price by applying tax, adding shipping costs, and then applying any available discounts.

```php
function calculate_final_price($base_price) {

  // Load the necessary modules
  $this->module("tax");
  $this->module("shipping");
  $this->module("discount");

  // Apply tax to the base price
  $price_with_tax = $this->tax->add_tax($base_price);

  // Add shipping costs
  $price_with_shipping = $this->shipping->add_shipping($price_with_tax);

  // Apply discounts
  $final_price = $this->discount->apply_discount($price_with_shipping);
  return $final_price;
}
```


In the example above:


- The 'Tax' module's `add_tax` method is used to add tax to the base price.
- The 'Shipping' module's `add_shipping` method calculates and adds the shipping cost to the price with tax.
- The 'Discount' module's `apply_discount` method applies any available discounts to the price with shipping.

> [!TIP]
> **Best Practices**
>
> In this example, the modules are loaded together at the beginning of the method. This approach enhances code readability and maintainability by clearly showing which modules are being used.


# Loading Modules From Views


Within the Trongate framework, it is possible to load another module from within a view file. This capability provides additional flexibility and allows for dynamic content generation within views.


To load a module from a view file, use the following syntax:

```vf
<?= Modules::run("module_name/method_name") ?>
```

## Why Use This Approach?


There are various scenarios where loading a module from within a view file can be advantageous. For instance, consider the need to include a 'Stripe' payment button on a webpage. When users click the 'Buy Now' button, a pop-up might appear, prompting the user to enter payment details. The implementation of such a feature can be complex and is best handled by a dedicated 'stripe' module.


Having a separate 'stripe' module that manages everything related to Stripe payments, including rendering the pop-up payment modal, allows you to maintain clean and organized code. This module can be easily called from any view file with a single line of code, as shown below:

```vf
<?= Modules::run("stripe/render_payment_button") ?>
```

## Passing Arguments


When calling modules from view files, arguments can be passed to the methods. This is done by separating the arguments with commas. Below is an example where a variable called `$name` is passed as an argument:

```vf
<?= Modules::run("welcome/greeting", $name) ?>
```

> [!NOTE]
> **Just To Let You Know...**
>
> The examples above use short PHP echo tags.  However, it's important to note that use normal (long) opening 
>     PHP tags would work also.  For example, the code below is valid:
> 
> ```vf
> <?php
> echo Modules::run("welcome/greeting", $name);
> ?>
> ```
> 
> 
> With regards to working with view files and HTML templates, Trongate favors pure PHP.


