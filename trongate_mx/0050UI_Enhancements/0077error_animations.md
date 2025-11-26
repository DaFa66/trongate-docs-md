# Error Animations


The `mx-animate-error` attribute triggers an error animation when an API endpoint returns an HTTP status code outside the 'success' range (i.e., not between 200 and 299).

## Demonstration


Click the button below to see an example of an 'error' animation:

Submit
## How It Works


The `mx-animate-error` attribute attaches an error animation to **elements initiating HTTP requests**, such as buttons or forms. When the request fails, users see an error animation, giving immediate feedback that the operation was unsuccessful.

### Example


Here's how you can implement `mx-animate-error`:

```vf
<?php
$form_attr = [
    'mx-post' => 'endpoint/submit_simulate_error',
    'mx-animate-error' => 'true'
];
echo form_open('#', $form_attr);
echo form_submit('save_btn', 'Save Changes');
echo form_close();
?>
```


For an HTML-only approach, here's the corresponding code:

```html
<form mx-post="endpoint/submit_simulate_error"
      mx-animate-error="true">
    <button type="submit">Save Changes</button>        
</form>
```


Here's a PHP method that can be used to return an 'error' response:

```php
public function submit_simulate_error() {
    http_response_code(400);
    die();
}
```


Clicking the submit button sends a POST request to `endpoint/submit_simulate_error`. If the request fails (HTTP status outside 200-299), the error animation is displayed over the form.

> [!WARNING]
> **Important:** The `mx-animate-error` attribute must be added to the element initiating the HTTP request. Adding it to unrelated elements will not trigger the animation.


## Syntax


The syntax for `mx-animate-error` is simple:

```html
<element mx-animate-error="true">
```


Setting the attribute value to "true" activates the animation.

## Placement Rules


The placement of the error animation depends on the context:


- **Default:** The animation appears inside the element that contains the `mx-animate-error` attribute.
- **Modals:** If the element that contains the `mx-animate-error` attribute is inside a modal, the animation will be rendered within the containing modal body - temporarily hiding the entire contents of the modal body.

> [!NOTE]
> **Just To Let You Know...**
>
> **Tip:** Use `mx-animate-error` alongside `mx-post` for a seamless combination of server-side operations and client-side feedback.


## Advanced Example


Here's a practical example combining `mx-animate-error` with other MX attributes:

```vf
<?php
$form_attr = [
    'mx-post' => 'submit_data',
    'mx-target' => '#response',
    'mx-animate-error' => 'true',
    'autocomplete' => 'off'
];

echo form_open('#', $form_attr);
echo form_label('Name');
echo form_input('name', '');
echo form_submit('submit_btn', 'Submit');
echo form_close();
?>

<div id="response"></div>
```


If you'd rather work directly with HTML, here's the code:

```html
<form mx-post="submit_data"
      mx-target="#response"
      mx-animate-error="true"
      autocomplete="off">
    <label>Name</label>        
    <input type="text" name="name">
    <button type="submit">Submit</button>
</form>

<div id="response"></div>
```

> [!CAUTION]
> Building web applications using pure HTML forms introduces potential security risks.  For more details, refer to our documentation pertaining to [CSRF Protection](documentation/display/trongate_mx/trongate-mx-security/csrf-protection)
> 
> 
> If in doubt, use Trongate's form helper functions whenever possible.



In this example:


1. The form submits data to `submit_data`.
2. Upon error, an error animation appears within the form.
3. After a second or two, the animation disappears.
4. The original form then reappears.

> [!NOTE]
> **Just To Let You Know...**
>
> The '**autocomplete**' attribute, when set to 'off' on a form's opening tag, prevents the browser from suggesting or automatically filling in previously entered values for any of the form fields. This is especially useful for forms that collect sensitive or unique information, as it ensures the browser won't try to pre-fill fields with stored data.


## Things To Keep In Mind


- The animation is purely client-side and does not confirm server-side changes.
- It works with clickable elements such as buttons and form elements.
- For advanced error handling, consider pairing with attributes like `mx-redirect-on-error`.

> [!TIP]
> **Best Practices**
>
> **Best Practices:**
> 
> 
> - Add `mx-animate-error="true"` to elements initiating HTTP requests.
> - Combine with `mx-post` for AJAX-driven forms or buttons.


## Summary


The `mx-animate-error` attribute provides immediate feedback for failed operations. It can be used with buttons, forms, or modals, and works alongside other Trongate MX attributes to create interactive experiences.

