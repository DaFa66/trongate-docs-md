# Building Dynamic Modals


The `mx-build-modal` attribute in Trongate MX allows you to dynamically create and populate modal dialogs with content fetched via AJAX. This feature lets you craft interactive, on-demand modal experiences without requiring pre-defined modal structures in your HTML.

## Demonstration


Click on the 'Create Modal' button to see a demonstration of dynamical modal creation.  The modal that is created will fetch the headline from the homepage of this website and insert the headline inside the modal body.

Create Modal
## Syntax

```html
<element mx-build-modal="modalOptions">
```


The `modalOptions` can either be a string (representing the modal ID) or a JSON object for detailed configuration.

## Basic Usage


Here's an example of using `mx-build-modal` with a string:

```vf
<?php
$btn_attr = [
    'mx-get' => 'api/get_user_info',
    'mx-build-modal' => 'user-info-modal'
];

echo form_button('view_btn', 'Build Modal', $btn_attr);
?>
```


Here's a pure HTML representation of the solution:

```html
<button mx-get="api/get_user_info" 
        mx-build-modal="user-info-modal">Build Modal</button>
```


Key details about this example:


- A modal with the ID "user-info-modal" is dynamically created upon clicking the button.
- Default modal settings are applied, including no close button and standard width.
- The modal body is populated with content fetched from the specified endpoint.

## Advanced Usage


For more precise control, use a JSON object to configure the modal:

```vf
<?php
$attr = [
  'mx-get' => 'title_boss/attempt_add_new_title',
  'mx-build-modal' => json_encode([
    'id' => 'add-element-modal',
    'width' => '460px',
    'marginTop' => '3vh',
    'modalHeading' => 'Add New Title',
    'showCloseButton' => 'true'
  ])
];
echo form_button('add_new_title_btn', 'Add New Title', $attr);
?>
```


For an HTML-only approach, here's the corresponding code:

```html
<button mx-get="title_boss/attempt_add_new_title" 
        mx-build-modal='{
            "id": "add-element-modal",
            "width": "460px",
            "marginTop": "3vh",
            "modalHeading": "Add New Title",
            "showCloseButton": "true"
        }'>Add New Title</button>
```


Key details about this advanced example:


- The modal is assigned a custom ID "add-element-modal".
- A specific width of 460px is applied.
- The modal appears 3vh from the top of the viewport.
- A modal heading with the text, 'Add New Title' is rendered.
- A close button is included for user convenience.
- Content is dynamically fetched from the "title_boss/attempt_add_new_title" endpoint.

## Modal Footers


Trongate MX gives you the ability to easily add beautiful modal footers onto dynamically generated modals.  These footers can contain anything you like.  However, a typical use case would be to have modal footers containing form submit buttons and, if required, 'Cancel' buttons.


Click the 'View Example' button below to see an example of a modal with a footer.

View Example

In order to have footer elements being added to dynamic modals, add a property of 'modalFooter' within the **mx-build-modal** attribute.  The 'modalFooter' property should be assigned with a value that represents the HTML code that is to be rendered within the modal footer.  For example:

```html
<button mx-get="documentation-demo/sample_form"   
        mx-build-modal='{
            "id": "demo-headline-modal",
            "width": "640px",
            "modalHeading": "Demonstration",
            "modalFooter": "<button class=\"alt\" onclick=\"closeModal()\">Cancel</button><button form=\"sample-form\">Submit</button>"
        }'>
    View Example
</button>
```

> [!NOTE]
> **Just To Let You Know...**
>
> In the example shown above, two buttons have been added inside the footer element.
> 
> 
> - We have a 'Cancel' button and, when clicked, it will close the modal.  This closing effect is achieved by adding: `onclick="closeModal()"` within the cancel button element.
> - The form 'Submit' button is technically not inside the form opening and closing tags within the rendered modal body.   However, in the example, the submit button has been associated with the form by giving the button an attribute of "form" with a value equal to the 'id' of the target form element.  In the example, the rendered form has an ID of 'sample-form'.  So, the button is associated with the form by adding, `form="sample-form"` to the submit button.
> 
> 
> **And Finally...**
> 
> 
> Don't forget to add backslashes when adding double quotes within the value that is being assigned to **modalFooter**!


## Modal Options


When using a JSON object, the following options are available:


- **id** (required): The modal's unique ID in the DOM.
- **width** (optional): Modal width (e.g., in px, %, or other CSS units).
- **marginTop**/**margin-top** (optional): Distance from the top of the viewport. Defaults to "12vh" if unspecified.
- **showCloseButton** (optional): Set to "true" to display a close button; omit or set to "false" to hide it.
- **modalHeading** (optional): HTML content for the modal heading.
- **modalFooter** (optional): HTML content for the modal footer.
- **renderCloseIcon** (optional): Controls whether a close icon appears when using modalHeading. Defaults to "true".

> [!NOTE]
> **Just To Let You Know...**
>
> **Important Note About Modal Headers**
> 
> 
> When using `mx-build-modal` with a `modalHeading` property, Trongate MX automatically adds a close icon (×) to the top-right corner of your modal window. The system detects whether Font Awesome is available in your project. If it is, Trongate MX will use the `fa-times` icon. If Font Awesome isn't available, the system automatically generates a similar-looking SVG close icon instead.
> 
> 
> **Controlling the Close Icon**
> 
> 
> If you don't want the close icon to appear automatically when using a `modalHeading`, you can prevent this by setting the 'renderCloseIcon' property to 'false' in your modal options. This will create a modal header without any close button.


## Additional Features


Extend modal functionality with these related attributes:


- **mx-close-on-success**: Closes the modal upon successful AJAX requests.
- **mx-close-on-error**: Closes the modal if an AJAX request fails.
- **mx-animate-success**: Adds a success animation after successful AJAX responses.
- **mx-animate-error**: Adds an error animation after failed AJAX responses.


For example:

```vf
<?php
$attr = [
  'mx-get' => 'title_boss/attempt_add_new_title',
  'mx-build-modal' => json_encode([
    'id' => 'add-element-modal',
    'width' => '460px',
    'margin-top' => '5vh',
    'showCloseButton' => 'true'
  ]),
  'mx-close-on-success' => 'true',
  'mx-animate-success' => 'true'
];

echo form_button('add_new_title_btn', '<i class="fa fa-plus-circle"></i> Attempt Add New Title', $attr);
?>
```


Alternatively, the same functionality can be achieved with pure HTML:

```html
<button mx-get="title_boss/attempt_add_new_title" 
        mx-build-modal='{
            "id": "add-element-modal",
            "width": "460px",
            "margin-top": "5vh",
            "showCloseButton": "true"
        }' 
        mx-close-on-success="true" 
        mx-animate-success="true">Attempt Add New Title</button>
```

## Additional Notes


- Modal styling is governed by your application's CSS - customise as needed.
- Fetched content is inserted directly into the modal body.
- `mx-target` can specify where fetched content should appear within the modal.
- Use `mx-on-success` or `mx-on-error` to handle AJAX responses.
- Both `marginTop` and `margin-top` are valid property names for top margin settings.


By combining `mx-build-modal` with other Trongate MX attributes, you can effortlessly create dynamic and engaging modal experiences.

