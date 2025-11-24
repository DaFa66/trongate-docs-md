# Form Display Methods


When integrating forms into your web application, Trongate MX offers three powerful approaches to form presentation: default display, modal windows, and hidden forms with triggers. Each method serves different user experience needs while maintaining the dynamic capabilities of Trongate MX.

## Default Display Method


The simplest approach is to display forms directly on the page load. This method works well for primary actions where form completion is the main goal.


Here's how to create a basic form using Trongate's helper functions:

```vf
<?php
$form_attr = [
    'mx-post' => 'users/create',
    'mx-target' => '#response'
];
echo form_open('#', $form_attr);
echo form_label('Username');
echo form_input('username', '');
echo form_label('Email');
echo form_input('email', '');
echo form_submit('submit', 'Create Account');
echo form_close();
?>
<div id="response"></div>
```


For those who prefer working with pure HTML, here's how to achieve the same result:

```html
<form mx-post="users/create" 
      mx-target="#response">
    <label>Username</label>
    <input type="text" name="username">
    <label>Email</label>
    <input type="text" name="email">
    <button type="submit">Create Account</button>
</form>
<div id="response"></div>
```

## Modal Window Forms


Modal windows create focused interactions by displaying forms in overlay dialogs. This approach is perfect for secondary actions that shouldn't disrupt the main content flow.


First, let's create a button to trigger the modal using Trongate's helper functions:

```vf
<?php
// Button to trigger the modal
$btn_attr = [
    'mx-get' => 'users/get_modal_form',
    'mx-build-modal' => json_encode([
        'id' => 'user-form-modal',
        'width' => '500px',
        'modalHeading' => 'Create Account',
        'showCloseButton' => 'true'
    ])
];
echo form_button('create_btn', 'Create Account', $btn_attr);
?>
```


Here's how you can accomplish the same using standard HTML:

```html
<button mx-get="users/get_modal_form"
        mx-build-modal='{
            "id": "user-form-modal",
            "width": "500px",
            "modalHeading": "Create Account",
            "showCloseButton": "true"
        }'>Create Account</button>
```

> [!NOTE]
> **Just To Let You Know...**
>
> Full documentation on how to build dynamic modals, with Trongate MX, is available [here](documentation/display/trongate_mx/ui-enhancements/building-dynamic-modals).



The corresponding view file for the modal content would look like this using helper functions:

```vf
<?php
$form_attr = [
    'mx-post' => $form_location,
    'mx-close-on-success' => 'true',
    'class' => 'text-center'
];
echo form_open('#', $form_attr);
echo form_label('Username');
echo form_input('username', '');
echo form_label('Email');
echo form_input('email', '');
echo form_submit('submit', 'Create Account');
echo form_close();
?>
```


To implement this using only HTML, see the example below:

```html
<form mx-post="users/create" 
      mx-close-on-success="true" 
      class="text-center">
    <label>Username</label>
    <input type="text" name="username">
    <label>Email</label>
    <input type="text" name="email">
    <button type="submit">Create Account</button>
</form>
```


And the controller method to serve the form:

```php
function get_modal_form() {
    // This method returns the HTML content that will populate the modal
    $data['form_location'] = 'users/create';
    
    // Load a view containing your form
    $this->view('users/modal_form', $data);
}
```

## Hidden Forms with Triggers


For a cleaner interface, forms can remain hidden until needed. This approach uses triggers to reveal forms dynamically.


Here's how to implement this using Trongate's helper functions:

```vf
<?php
// Button to reveal the form
$btn_attr = [
    'mx-get' => 'users/get_form',
    'mx-target' => '#form-container'
];
echo form_button('show_form', 'Show Form', $btn_attr);
?>
<div id="form-container"></div>
```


For a pure HTML approach, here's the corresponding code:

```html
<button mx-get="users/get_form"
        mx-target="#form-container">Show Form</button>
<div id="form-container"></div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> ### Best Practices for Form Display
> 
> 
> - Use default display for primary page actions where form completion is the main goal.
> - Choose modals for secondary actions that require focused attention.
> - Implement hidden forms when you want to preserve space and provide progressive disclosure.
> - Always ensure clear visual feedback when forms are shown or hidden.


## Summary


Trongate MX provides flexible options for displaying forms, each suited to different scenarios. The default display method works well for primary forms, while modal windows create focused interactions for secondary tasks. Hidden forms with triggers help maintain a clean interface while providing progressive disclosure. By choosing the right display method and implementing it with Trongate MX's intuitive attributes, you can create engaging and user-friendly form experiences.

