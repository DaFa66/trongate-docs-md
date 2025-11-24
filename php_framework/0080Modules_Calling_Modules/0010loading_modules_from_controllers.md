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


