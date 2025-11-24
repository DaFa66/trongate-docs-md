# Understanding Parent and Child Modules


The Trongate framework introduces the concept of Parent and Child Modules, a powerful feature that allows for modular and hierarchical organization of application components. This architecture enables developers to create complex, nested module structures, enhancing code reusability and maintaining a clean, organized codebase.

## Key Concepts


- **Parent Module:** A module that contains one or more child modules.
- **Child Module:** A module that is nested within a parent module.


This hierarchical structure allows for the creation of self-contained, feature-rich components that can be easily integrated into Trongate applications.

## Structuring Parent and Child Modules


When working with parent and child modules in Trongate, it's essential to understand the proper directory structure and naming conventions.

### Directory Structure

```
modules/
├── parent_module/
│   ├── controllers/
│   ├── assets/
│   ├── views/
│   └── child_module/
│       ├── controllers/
│       ├── assets/
│       └── views/
```


In this structure, the child module is a subdirectory within its parent module, maintaining its own = anchor('basic-concepts/truly-modular-architecture.html', 'truly modular') ?> structure.

### Naming Conventions


When referencing child modules, use the format: `parent_module-child_module`. This convention is crucial for proper routing and module loading.

# Accessing Child Modules


Trongate provides multiple ways to access and utilize child modules within your application.

## URL Routing


To access a child module via URL, use the following format:

```php
http://your-domain.com/parent_module-child_module/method
```

### Example #1


The code sample below demonstrates how to access the 'display' method of an 'accessories' child module within a 'cars' parent module:

```php
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
    $latest_reviews = $this->product_reviews->get_latest_reviews($product_id, 5);

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


In this example, we first load the 'product_reviews' child module using `$this->module('shop-product_reviews')`. After loading, we can access the child module's methods using `$this->product_reviews->method_name()`. Here, we're calling the `get_latest_reviews()` method to fetch the five most recent reviews for a specific product.

