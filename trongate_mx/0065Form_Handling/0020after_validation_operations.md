# After Validation Operations


The `mx-after-validation` attribute in Trongate MX allows you to execute custom JavaScript functions immediately after form validation errors are displayed.

## Usage


Here's a simple example showing how to use the `mx-after-validation` attribute:

```vf
<?php
$form_attributes = [
    'class' => 'highlight-errors',
    'mx-post' => 'api/users/create',
    'mx-after-validation' => 'showErrorCount'
];
echo form_open('', $form_attributes);
echo '<div id="error-summary"></div>';
echo form_input('username');
echo form_input('email');
echo form_submit('submit', 'Create User');
echo form_close();
?>

<script>
function showErrorCount() {
    const errorFields = document.querySelectorAll('.form-field-validation-error');
    const errorSummary = document.getElementById('error-summary');
    const count = errorFields.length;
    
    errorSummary.innerHTML = `<div class="alert alert-danger">
        Please correct the ${count} error${count !== 1 ? 's' : ''} below
    </div>`;
}
</script>
```


When the form is submitted with invalid data, Trongate MX automatically displays validation errors next to the relevant form fields. Once these errors are displayed, the `showErrorCount` function is called. In this example, it counts the validation errors and displays a summary message to help users understand how many issues need to be addressed.

### Alternative Syntax


If you prefer working directly with HTML instead of using Trongate's form helpers, here's the equivalent code:

```html
<form class="highlight-errors"
      mx-post="api/users/create"
      mx-after-validation="showErrorCount">
    <div id="error-summary"></div>
    <input type="text" name="username">
    <input type="email" name="email">
    <button type="submit">Create User</button>
</form>

<script>
function showErrorCount() {
    const errorFields = document.querySelectorAll('.form-field-validation-error');
    const errorSummary = document.getElementById('error-summary');
    const count = errorFields.length;
    
    errorSummary.innerHTML = `<div class="alert alert-danger">
        Please correct the ${count} error${count !== 1 ? 's' : ''} below
    </div>`;
}
</script>
```

## More Examples

### Custom Error Styling


You might want to draw attention to validation errors when they appear. Here's how you can temporarily make erroneous fields blink:

```vf
<?php
$form_attributes = [
    'class' => 'highlight-errors',
    'mx-post' => 'api/products/create',
    'mx-after-validation' => 'highlightErrors'
];
echo form_open('', $form_attributes);
echo form_input('product_name');
echo form_textarea('description');
echo form_submit('submit', 'Add Product');
echo form_close();
?>

<script>
function highlightErrors() {
    // Add blink class to all error fields
    const errorFields = document.querySelectorAll('.form-field-validation-error');
    errorFields.forEach(field => {
        field.classList.add('blink');
    });

    // Remove blink class after 3 seconds
    setTimeout(() => {
        errorFields.forEach(field => {
            field.classList.remove('blink');
        });
    }, 3000);
}
</script>
```

> [!NOTE]
> **Just To Let You Know...**
>
> ###  Understanding the customEvent Parameter
> 
> 
> When Trongate MX calls your validation handler function, it passes a `customEvent` parameter containing useful information about the validation event. The `customEvent.detail` object includes:
> 
> 
> - `element`: The form element that triggered the validation
> - `originalEvent`: The original form submission event
> 
> 
> You only need to include this parameter if you plan to use this contextual information in your handler function.


### Analytics and Error Tracking


You can use `mx-after-validation` to track validation errors for analytics or debugging purposes. This example demonstrates using the `customEvent` parameter to access form information:

```vf
<?php
$form_attributes = [
    'class' => 'highlight-errors',
    'mx-post' => 'api/orders/submit',
    'mx-after-validation' => 'trackValidationErrors'
];
echo form_open('', $form_attributes);
// Add your form fields here
echo form_close();
?>

<script>
function trackValidationErrors(customEvent) {
    const errorFields = document.querySelectorAll('.form-field-validation-error');
    const errorMessages = document.querySelectorAll('.validation-error-report');
    
    // Log validation issues
    console.log('Form validation failed');
    console.log('Number of errors:', errorFields.length);
    
    // You could send this to your analytics service
    const errorData = {
        timestamp: new Date().toISOString(),
        formId: customEvent.detail.element.id,
        errorCount: errorFields.length,
        fields: Array.from(errorFields).map(field => field.name)
    };
    
    // Example: assuming you have a sendToAnalytics() function defined
    sendToAnalytics('form_validation_error', errorData);
}
</script>
```

> [!TIP]
> **Best Practices**
>
> - **Validation Context:** The function receives a customEvent parameter with validation details
> - **Error Elements:** Use `.form-field-validation-error` to find invalid fields
> - **Error Messages:** Find error messages in `.validation-error-report` elements
> - **User Experience:** Focus on helping users correct their input efficiently


## Summary


The `mx-after-validation` attribute provides a powerful way to customize how your application handles form validation errors. By executing JavaScript after validation errors are displayed, you can enhance the user experience with custom animations, helpful UI behaviors, and error tracking capabilities. This makes form validation more user-friendly and helps you maintain better insight into validation issues in your application.

