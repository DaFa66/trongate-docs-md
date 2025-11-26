# Success Animations


The `mx-animate-success` attribute triggers a checkmark animation when an API endpoint returns an HTTP success status code that's in the 'success' range (i.e., 200 - 299).

## Demonstration


Click the button below to see an example of a 'success' animation:

Submit
## How It Works


The `mx-animate-success` attribute attaches a success animation to **elements initiating HTTP requests**, such as buttons or forms. When the request succeeds, users see a checkmark animation, giving immediate feedback that the operation was successful.

### Example


Here's how you can implement `mx-animate-success`:

```vf
<?php
$form_attr = [
    'mx-post' => 'endpoint/submit',
    'mx-animate-success' => 'true'
];
echo form_open('#', $form_attr);
echo form_submit('save_btn', 'Save Changes');
echo form_close();
?>
```


For an HTML-only approach, here's the corresponding code:

```html
<form mx-post="endpoint/submit" mx-animate-success="true">
    <button type="submit">Save Changes</button>
</form>
```


Clicking the submit button sends a POST request to `endpoint/submit`. If the request succeeds (HTTP status 200-299), the checkmark animation is displayed over the form.

> [!WARNING]
> **Important:** The `mx-animate-success` attribute must be added to the element initiating the HTTP request. Adding it to unrelated elements will not trigger the animation.


## Syntax


The syntax for `mx-animate-success` is simple:

```html
<element mx-animate-success="true">
```


Setting the attribute value to "true" activates the animation.

## Placement Rules


The placement of the success animation depends on the context:


- **Default:** The animation appears inside the element that contains the `mx-animate-success` attribute.
- **Modals:** If the element that contains the `mx-animate-success` attribute is inside a modal, the animation will be rendered within the containing modal body - temporarily hiding the entire contents of the modal body.

> [!NOTE]
> **Just To Let You Know...**
>
> **Tip:** Use `mx-animate-success` alongside `mx-post` for a seamless combination of server-side operations and client-side feedback.


## Advanced Example


Here's a practical example combining `mx-animate-success` with other MX attributes:

```vf
<?php
$form_attr = [
    'mx-post' => 'submit_data',
    'mx-target' => '#response',
    'mx-animate-success' => 'true',
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


If you'd rather work with pure HTML, here's the code:

```html
<form mx-post="submit_data"
      mx-target="#response"
      mx-animate-success="true"
      autocomplete="off">
  <label>Name</label>         
  <input type="text" name="name">
  <button type="submit">Submit</button>
</form>

<div id="response"></div>
```


In this example:


1. The form submits data to `submit_data` via AJAX.
2. Upon success, a checkmark animation appears within the form.
3. After a second or two, the animation disappears.
4. The response text, from the API, is then inserted inside the `#response` element.

> [!NOTE]
> **Just To Let You Know...**
>
> The '**autocomplete**' attribute, when set to 'off' on a form's opening tag, prevents the browser from suggesting or automatically filling in previously entered values for any of the form fields. This is especially useful for forms that collect sensitive or unique information, as it ensures the browser won't try to pre-fill fields with stored data.


## Things To Keep In Mind


- The animation is purely client-side and does not confirm server-side changes.
- It works with clickable elements such as buttons and form elements.
- For advanced error handling, consider pairing with attributes like `mx-redirect-on-error`.

## Summary


The `mx-animate-success` attribute provides immediate feedback for successful operations. It can be used with buttons, forms, or modals, and works alongside other Trongate MX attributes to create interactive experiences.

> [!TIP]
> **Best Practices**
>
> **Best Practices:**
> 
> 
> - Add `mx-animate-success="true"` to elements initiating HTTP requests.
> - Combine with `mx-post` for AJAX-driven forms or buttons.


