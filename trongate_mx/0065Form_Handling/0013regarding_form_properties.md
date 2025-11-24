# Regarding Form Attributes


While Trongate MX enhances form handling with dynamic features, it's important to understand how to leverage HTML5's built-in form validation attributes and other useful form properties. These attributes can improve user experience by providing immediate feedback before form submission.

## Making Fields Required


To make specific fields required in your form, add the 'required' attribute to individual form elements:


Here's how to implement this using Trongate's helper functions:

```vf
<?php
$form_attr = [
    'mx-post' => 'users/create'
];
echo form_open('#', $form_attr);

$username_attr = [
    'required' => 'true'
];
echo form_label('Username');
echo form_input('username', '', $username_attr);

$email_attr = [
    'required' => 'true'
];
echo form_label('Email');
echo form_input('email', '', $email_attr);

// This field is optional
echo form_label('Phone');
echo form_input('phone', '');

echo form_submit('submit', 'Create Account');
echo form_close();
?>
```


For those who prefer working directly with HTML, here's how to achieve the same functionality:

```html
<form mx-post="users/create">
    <label>Username</label>
    <input type="text" name="username" required>
    
    <label>Email</label>
    <input type="text" name="email" required>
    
    <label>Phone</label>
    <input type="text" name="phone">
    
    <button type="submit">Create Account</button>
</form>
```

## Setting Input Lengths


You can control the minimum and maximum length of text input fields:


Using Trongate's form helper functions:

```vf
<?php
$form_attr = [
    'mx-post' => 'users/create'
];
echo form_open('#', $form_attr);

$username_attr = [
    'required' => 'true',
    'minlength' => '3',
    'maxlength' => '30'
];
echo form_label('Username (3-30 characters)');
echo form_input('username', '', $username_attr);

$bio_attr = [
    'maxlength' => '200'
];
echo form_label('Bio (max 200 characters)');
echo form_textarea('bio', '', $bio_attr);

echo form_submit('submit', 'Create Account');
echo form_close();
?>
```


Here's the same implementation using straightforward HTML:

```html
<form mx-post="users/create">
    <label>Username (3-30 characters)</label>
    <input type="text" 
           name="username" 
           required 
           minlength="3" 
           maxlength="30">
    
    <label>Bio (max 200 characters)</label>
    <textarea name="bio" 
              maxlength="200"></textarea>
    
    <button type="submit">Create Account</button>
</form>
```

## Numeric Input Ranges


For numeric inputs, you can specify acceptable minimum and maximum values:


Here's the implementation using Trongate's helper functions:

```vf
<?php
$form_attr = [
    'mx-post' => 'products/create'
];
echo form_open('#', $form_attr);

$quantity_attr = [
    'required' => 'true',
    'min' => '1',
    'max' => '100'
];
echo form_label('Quantity (1-100)');
echo form_number('quantity', '', $quantity_attr);

$price_attr = [
    'required' => 'true',
    'min' => '0.01',
    'max' => '9999.99'
];
echo form_label('Price ($0.01 - $9999.99)');
echo form_number('price', '', $price_attr);

echo form_submit('submit', 'Add Product');
echo form_close();
?>
```


To achieve this using pure HTML, here's the equivalent code:

```html
<form mx-post="products/create">
    <label>Quantity (1-100)</label>
    <input type="number" 
           name="quantity" 
           required 
           min="1" 
           max="100">
    
    <label>Price ($0.01 - $9999.99)</label>
    <input type="number" 
           name="price" 
           required 
           min="0.01" 
           max="9999.99">
    
    <button type="submit">Add Product</button>
</form>
```

## Autocomplete Settings


The autocomplete attribute controls whether browsers should offer to save and auto-fill form data. This can be particularly important for login forms and sensitive information:


First, let's look at how to implement this using Trongate's helper functions:

```vf
<?php
// Example 1: Disable autocomplete for the entire form
$form_attr = [
    'mx-post' => 'users/login',
    'autocomplete' => 'off'
];
echo form_open('#', $form_attr);
echo form_label('Username');
echo form_input('username', '');
echo form_label('Password');
echo form_password('password', '');
echo form_submit('submit', 'Login');
echo form_close();

// Example 2: Enable autocomplete but with specific field behaviors
$form_attr = [
    'mx-post' => 'users/register'
];
echo form_open('#', $form_attr);

// Encourage browsers to suggest a new password
$password_attr = [
    'autocomplete' => 'new-password'
];
echo form_label('Choose Password');
echo form_password('password', '', $password_attr);

// Allow autocomplete for non-sensitive information
$email_attr = [
    'autocomplete' => 'email'
];
echo form_label('Email');
echo form_input('email', '', $email_attr);

echo form_submit('submit', 'Register');
echo form_close();
?>
```


Here's how to achieve the same functionality using standard HTML:

```html
<!-- Example 1: Disable autocomplete for the entire form -->
<form mx-post="users/login" autocomplete="off">
    <label>Username</label>
    <input type="text" name="username">
    <label>Password</label>
    <input type="password" name="password">
    <button type="submit">Login</button>
</form>

<!-- Example 2: Enable autocomplete with specific field behaviors -->
<form mx-post="users/register">
    <label>Choose Password</label>
    <input type="password" 
           name="password" 
           autocomplete="new-password">
    
    <label>Email</label>
    <input type="text" 
           name="email" 
           autocomplete="email">
    
    <button type="submit">Register</button>
</form>
```

> [!NOTE]
> **Just To Let You Know...**
>
> ### Common Validation Attributes:
> 
> 
> - `required`: Field must be filled out before submission
> - `minlength`: Minimum number of characters for text input
> - `maxlength`: Maximum number of characters for text input
> - `min`: Minimum value for numeric inputs
> - `max`: Maximum value for numeric inputs
> - `pattern`: Regular expression pattern for validation


> [!NOTE]
> **Just To Let You Know...**
>
> ### Autocomplete Values:
> 
> 
> - `off`: Suggests that browsers should not automatically enter or select a value for this field
> - `new-password`: Indicates this field is for a new password, helping password managers suggest strong passwords
> - `email`: Indicates this field expects an email address
> - `tel`: Indicates this field expects a telephone number


## Summary


HTML form attributes and client-side validation provide an essential first line of defense against invalid data while improving user experience. While client-side validation enhances user experience, remember to always implement server-side validation for security. Each validation attribute serves a specific purpose, and using them appropriately helps create more user-friendly forms.

