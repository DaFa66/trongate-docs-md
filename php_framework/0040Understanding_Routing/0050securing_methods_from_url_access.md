# Securing Methods


Trongate provides a straightforward way to protect controller methods from direct URL access while keeping them available for internal use. This is crucial for maintaining application security.

## Using the Underscore Prefix


To prevent direct URL access to a method, prefix it with an underscore (_):

```php
<?php
class Store extends Trongate {

    // Publicly accessible
    public function products() {
        $items = $this->_fetch_products();
        $this->template('store/products', ['items' => $items]);
    }

    // Protected from URL access
    public function _fetch_products() {
        return $this->model->get('products');
    }
}
```

## Method Access Rules


| Method Type | URL Access | Internal Access | Example Usage |
| ---|---|---|---|
| Public Method | ✓ Allowed | ✓ Allowed | `function products()` |
| Underscore Method | ✗ Blocked | ✓ Allowed | `function _process_form()` |

## Common Use Cases

### Form Processing

```php
<?php
class Users extends Trongate {
    
    // Public form display
    public function register() {
        $this->template('users/register_form');
    }
    
    // Protected processing method
    public function _process_registration() {
        // Process form data
        // Validate inputs
        // Create user account
    }
}
```

### API Methods

```php
<?php
class Products extends Trongate {
    
    // Public API endpoint
    public function api() {
        $products = $this->_get_filtered_products();
        echo json_encode($products);
    }
    
    // Protected helper method
    public function _get_filtered_products() {
        // Apply filters
        // Return product data
    }
}
```

## Security Implications

> [!WARNING]
> **Warning!**
>
> **Important:** The underscore prefix only prevents URL access. These methods can still be called from within your application code using `$this->_method_name()`.


## Best Practices


- **Protect Data Processing:** Use underscore prefix for methods that handle sensitive operations or data processing
- **Helper Methods:** Internal helper methods should always use the underscore prefix
- **Form Handlers:** Methods that process form submissions should be protected
- **API Internals:** Internal API operations should use protected methods

## Method Organization


A well-organized controller might look like this:

```php
<?php
class Orders extends Trongate {
    
    // Public Methods (URL Accessible)
    public function create() {
        // Show order form
    }
    
    public function view($order_id) {
        // Display order details
    }
    
    // Protected Methods (Internal Only)
    public function _validate_order($data) {
        // Validation logic
    }
    
    public function _process_payment($order_data) {
        // Payment processing
    }
    
    public function _send_confirmation($order_id) {
        // Email confirmation
    }
}
```


This organization makes it clear which methods are part of your public interface and which are for internal use only.

