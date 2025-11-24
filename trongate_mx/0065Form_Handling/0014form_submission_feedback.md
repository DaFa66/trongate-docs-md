# Form Submission Feedback


When a form is submitted in Trongate MX, several automatic behaviors and visual feedback options help create a smooth user experience. This page explores the built-in features and customization options available during form submission.

## Automatic Form Behaviors


When a form is submitted, Trongate MX automatically:


- Disables all form elements to prevent double submission.
- Re-enables the form elements once a response is received.
- Clears any existing validation errors from previous submissions.


These behaviors require no additional attributes - they're built into Trongate MX's form handling system.

## Loading Indicators


Loading indicators provide visual feedback that a form submission is in progress. Here's how to implement this using Trongate's helper functions:

```vf
<?php
$form_attr = [
    'mx-post' => 'store/create',
    'mx-indicator' => '#submit-spinner'
];
echo form_open('#', $form_attr);
echo form_label('Product Name');
echo form_input('product_name', '');
echo form_submit('submit', 'Create Product');
echo form_close();
?>

<div id="submit-spinner" class="spinner mx-indicator"></div>
```


For those who prefer working with pure HTML, here's the equivalent implementation:

```html
<form mx-post="store/create"
      mx-indicator="#submit-spinner">
    <label>Product Name</label>
    <input type="text" name="product_name">
    <button type="submit">Create Product</button>
</form>

<div id="submit-spinner" class="spinner mx-indicator"></div>
```


The spinner automatically appears during form submission and hides when complete. The `mx-indicator` class ensures proper initialization and cleanup.

## Target Element Control


You can control how the form appears during submission using `mx-target-loading`. Two approaches are available:

### 1. Cloaking the Form


Here's how to implement form cloaking using Trongate's helper functions:

```vf
<?php
$form_attr = [
    'mx-post' => 'store/create',
    'mx-target-loading' => 'cloak'
];
echo form_open('#', $form_attr);
echo form_label('Product Name');
echo form_input('product_name', '');
echo form_submit('submit', 'Create Product');
echo form_close();
?>
```


To achieve the same cloaking effect using standard HTML:

```html
<form mx-post="store/create"
      mx-target-loading="cloak">
    <label>Product Name</label>
    <input type="text" name="product_name">
    <button type="submit">Create Product</button>
</form>
```

### 2. Showing a Loading Message


Using Trongate's form helper functions:

```vf
<?php
// First, create a hidden message
echo '<div id="loading-message" style="display: none;">';
echo '<div class="blink">Submitting your product...</div>';
echo '</div>';

// Then reference it in the form
$form_attr = [
    'mx-post' => 'store/create',
    'mx-target-loading' => '#loading-message'
];
echo form_open('#', $form_attr);
echo form_label('Product Name');
echo form_input('product_name', '');
echo form_submit('submit', 'Create Product');
echo form_close();
?>
```


Here's how to implement the loading message using pure HTML:

```html
<div id="loading-message" style="display: none;">
    <div class="blink">Submitting your product...</div>
</div>

<form mx-post="store/create"
      mx-target-loading="#loading-message">
    <label>Product Name</label>
    <input type="text" name="product_name">
    <button type="submit">Create Product</button>
</form>
```

## Combining Multiple Feedback Methods


You can combine different feedback methods for a comprehensive user experience. Here's how to do it using Trongate's helper functions:

```vf
<?php
// Hidden loading message
echo '<div id="loading-message" style="display: none;">';
echo '<div class="blink">Processing Your Submission</div>';
echo '</div>';

// Form with multiple feedback methods
$form_attr = [
    'mx-post' => 'store/create',
    'mx-target-loading' => '#loading-message',
    'mx-indicator' => '#submit-spinner'
];

echo form_open('#', $form_attr);
echo form_label('Product Name');
echo form_input('product_name', '');
echo form_submit('submit', 'Create Product');
echo form_close();
?>

<div id="submit-spinner" class="spinner mx-indicator"></div>
```


Here's the same comprehensive feedback implementation in straightforward HTML:

```html
<div id="loading-message" style="display: none;">
    <div class="blink">Processing Your Submission</div>
</div>

<form mx-post="store/create"
      mx-target-loading="#loading-message"
      mx-indicator="#submit-spinner">
    <label>Product Name</label>
    <input type="text" name="product_name">
    <button type="submit">Create Product</button>
</form>

<div id="submit-spinner" class="spinner mx-indicator"></div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> When using `mx-indicator` with forms, place the loading indicator outside the form to ensure it remains visible when the form elements are disabled.


## Response Handling


After submission, Trongate MX automatically:


- Re-enables all form elements.
- Hides loading indicators.
- Restores original content if using `mx-target-loading`.
- Displays any validation errors if they exist.

> [!TIP]
> **Best Practices**
>
> When building or testing API integrations, you can use PHP's `sleep()` function to simulate realistic network latency. This is particularly useful for testing features like loading indicators, ensuring they appear correctly during delayed server responses.
> 
> 
> For example, here's how you can introduce a 2-second delay to mimic a slow API response:
> 
> ```php
> function test() {
>   sleep(2);
>   http_reponse_code(200);
>   echo 'Hello from the API!';
> }
> ```


## Summary


Trongate MX provides a robust set of tools for handling form submissions gracefully. The automatic form element disabling prevents double submissions, while visual feedback options like loading indicators and content replacement keep users informed of the submission status. By combining these features, you can create form submissions that are both user-friendly and resilient.

