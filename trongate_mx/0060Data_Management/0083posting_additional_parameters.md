# Posting Additional Parameters


The `mx-vals` attribute in Trongate MX allows you to attach additional values to your HTTP requests as if they were submitted as part of an ordinary HTML form.

## Syntax Options


The `mx-vals` attribute requires a JSON object where each key-value pair represents a form field and its value. Here are the different ways to use this attribute:

### 1. Direct JSON String


Using Trongate's form helper functions:

```vf
<?php
$btn_attr = [
    'mx-post' => 'cart/add_item',
    'mx-vals' => '{"item_id": 123, "quantity": 2}'
];
echo form_button('add_to_cart_btn', 'Add to Cart', $btn_attr);
?>
```


Pure HTML equivalent:

```html
<button mx-post="cart/add_item"
        mx-vals='{"item_id": 123, "quantity": 2}'>
    Add to Cart
</button>
```

### 2. Using PHP's json_encode()


Using Trongate's form helper functions:

```vf
<?php
$btn_attr = [
    'mx-post' => 'cart/add_item',
    'mx-vals' => json_encode(['item_id' => 123, 'quantity' => 2])
];
echo form_button('add_to_cart_btn', 'Add to Cart', $btn_attr);
?>
```


Pure HTML equivalent:

```html
<button mx-post="cart/add_item"
        mx-vals='{"item_id": 123, "quantity": 2}'>
    Add to Cart
</button>
```

### 3. Using Predefined Arrays (Recommended)


Using Trongate's form helper functions:

```vf
<?php
$mx_vals = [
    'item_id' => 123,
    'quantity' => 2,
    'timestamp' => time()
];

$btn_attr = [
    'mx-post' => 'cart/add_item',
    'mx-vals' => json_encode($mx_vals)
];
echo form_button('add_to_cart_btn', 'Add to Cart', $btn_attr);
?>
```


Pure HTML equivalent:

```html
<button mx-post="cart/add_item"
        mx-vals='{"item_id": 123, "quantity": 2, "timestamp": 1703116800}'>
    Add to Cart
</button>
```

## Usage with Forms


The `mx-vals` attribute is particularly powerful when combined with form submissions. Here's a complete example:


Using Trongate's form helper functions:

```vf
<?php
// Define additional values to be sent with the form
$mx_vals = [
    'last_name' => 'Doe',
    'age' => 30
];

// Create form attributes
$form_attr = [
    'mx-post' => 'test/submit',
    'mx-vals' => json_encode($mx_vals)
];

// Build the form
echo form_open('#', $form_attr);
echo form_input('first_name', 'David', array('placeholder' => 'Enter your first name here....'));
echo form_submit('submit_btn', 'Submit');
echo form_close();
?>
```


Pure HTML equivalent:

```html
<form mx-post="test/submit"
      mx-vals='{"last_name": "Doe", "age": 30}'>
    <input type="text" 
           name="first_name" 
           value="David" 
           placeholder="Enter your first name here....">
    <button type="submit">Submit</button>
</form>
```


When this form is submitted, it will send:


- The visible form field (`first_name`).
- The additional values defined in `mx-vals` (`last_name` and `age`).

## Server-Side Handling


Here's how to handle the submitted data in your PHP endpoint:

```vf
<?php
public function submit() {
    $first_name = post('first_name');  // From visible form field
    $last_name = post('last_name');    // From mx-vals
    $age = post('age');                // From mx-vals
    
    // Process the data...
}
?>
```

## Technical Details


- Values from `mx-vals` are merged with regular form data before the request is sent.
- Both visible form fields and mx-vals values are accessible using the same methods on the server.
- In case of naming conflicts, the last value processed takes precedence.

> [!TIP]
> **Best Practices**
>
> 1. **Use json_encode()**
> - Prefer `json_encode()` over manual JSON string construction.
> - Helps prevent syntax errors and ensures proper escaping.
> 
> 
> 2. **Organize Values**
> - Define mx-vals arrays separately for better code organization.
> - Makes it easier to modify values dynamically.
> 
> 
> 3. **Value Types**
> - Numbers don't need quotes: `"age": 30`.
> - Booleans are supported: `"is_active": true`.
> - Strings must use double quotes: `"name": "John"`.
> 
> 
> 4. **Security**
> - Always validate mx-vals data on the server side.
> - Don't trust client-side values for critical operations.
> - Use appropriate data types and validation rules.


## Common Pitfalls to Avoid


- Don't use single quotes for JSON property names.
- Don't use unquoted property names.
- Don't use PHP array notation directly in the mx-vals value.
- Don't use array syntax instead of object syntax.

## Error Handling


If the JSON in mx-vals is invalid:


- An error will be logged to the browser console.
- The values will not be included in the request.
- The rest of the form submission will proceed normally.

## Summary


The `mx-vals` attribute provides a powerful way to include additional data with your HTTP requests in Trongate MX. Whether you're adding hidden parameters to a button click or combining additional data with form submissions, mx-vals offers flexibility and convenience. By using PHP's `json_encode()` with predefined arrays, you can maintain clean, organized code while ensuring all your required data is properly transmitted to your server endpoints.

