# Accessing Child Modules


Trongate provides multiple ways to access and utilize child modules within your application.

## URL Routing


To access a child module via URL, use the following format:

```
http://your-domain.com/parent_module-child_module/method
```

### Example #1


The code sample below demonstrates how to access the 'display' method of an 'accessories' child module within a 'cars' parent module:

```
http://your-domain.com/cars-accessories/display
```


---

## Creating Links

### Example #2


The code sample below demonstrates how to use the Trongate anchor() function to create links to child module methods:

```php
<?= anchor('cars-accessories/display', 'View Accessories') ?>
```


---

## Loading Child Modules Programmatically


To load a child module within a controller or another module:

```php
$this->module('parent_module-child_module');
$this->child_module->method();
```

### Example #3


This example demonstrates how to load and use a child module named 'product_reviews' within a parent module 'shop'. We'll load the child module and then call its 'get_latest_reviews' method:

```php
<?php
class Shop extends Trongate {

  function display_product($product_id) {

    // Load the product_reviews child module
    $this->module('shop-product_reviews');

    // Get the latest reviews for this product
    $latest_reviews = $this->product_reviews->get_latest_reviews($product_id);

    // Prepare data for the view
    $data['product_id'] = $product_id;
    $data['latest_reviews'] = $latest_reviews;
    $data['view_module'] = 'shop';
    $data['view_file'] = 'display_product';

    // Load the template, passing in the $data array
    $this->template('public', $data);
  }
}
```


In this example, the 'product_reviews' child module is loaded using:

```php
$this->module('shop-product_reviews');
```


Thereafter, the child module's methods can be accessed using syntax of the following form:

```php
$this->product_reviews->method_name();
```

> [!NOTE]
> **Just To Let You Know...**
>
> In the line of code above, `method_name` would be replaced with a meaningful and valid method name.  The method name would reference a method within the `product_reviews` module.



The example shown above fetches reviews, passing in the `$product_id` as an argument:

```php
$latest_reviews = $this->product_reviews->get_latest_reviews($product_id);
```

> [!TIP]
> **Best Practices**
>
> For a more robust and modern coding style, consider using access modifiers, doc blocks, type hinting and return types.  For example:
> 
> ```php
> <?php
> class Shop extends Trongate {
> 
>   /**
>    * Displays the product along with its latest reviews.
>    *
>    * @param mixed $product_id The product ID from the URL, which will be cast to an integer.
>    * @return void
>    */
>   public function display_product(mixed $product_id): void {
>     // Ensure $product_id is an integer
>     settype($product_id, 'int');
> 
>     // Load the product_reviews child module
>     $this->module('shop-product_reviews');
> 
>     // Get the latest reviews for this product
>     $latest_reviews = $this->product_reviews->get_latest_reviews($product_id);
> 
>     // Prepare data for the view
>     $data['product_id'] = $product_id;
>     $data['latest_reviews'] = $latest_reviews;
>     $data['view_module'] = 'shop';
>     $data['view_file'] = 'display_product';
> 
>     // Load the template, passing in the $data array
>     $this->template('public', $data);
>   }
> }
> ```
> 
> 
> In the code sample above we have a type hinting value set to 'mixed'.  This is because the `display_product()` method is attempting to read the `$product_id` from the third segment of the URL.  The expectation is that the  `$product_id` will be an integer.  However, if it's not then certainly don't want the code to break!  For this reason, we set the type to an integer with:
> 
> ```php
> settype($product_id, 'int');
> ```
> 
> 
> The following line of code would have achieved the same effect (making sure `$product_id` is an integer:
> 
> ```php
> $product_id = (int) $product_id;
> ```


