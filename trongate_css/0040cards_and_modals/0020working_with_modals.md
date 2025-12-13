# Working With Modals


Modals are popup dialogs that appear over the main content of a webpage. The Trongate ecosystem provides elegant modal styling along with JavaScript functionality for seamless modal interactions.  Click the button below to see an example of a basic modal:

Click Me!
Example Modal
This is an example modal. It has a default margin top value of '12vh', which is defined as a CSS variable within Trongate CSS.


The source code for this particular modal is hard-coded into the HTML of the webpage that you are currently viewing.


Close
## Basic Modal Structure


A basic modal consists of a heading and body section. Here's the standard structure:

```html
<div class="modal" id="example-modal" style="display: none">
    <div class="modal-heading">
        Important Notice
    </div>
    <div class="modal-body">
        <p>This is an example modal. In practice, modals would be triggered by JavaScript and appear as overlays.</p>
        <p class="text-center">
            <button class="alt" onclick="closeModal()">Close</button>
        </p>
    </div>
</div>
```

## Setting Up Modals


To use modals in your project, follow these steps:


1. Ensure you've included an appropriate JavaScript file (app.js/admin.js/trongate-mx.js) in your project.
2. Using `style="display: none"` to hide your modal element upon initial page load.
3. Add a trigger element (like a button) that calls `openModal()`, passing in the 'id' of the modal element that you'd like to have opened.


Here's a complete example:

```html
<!-- Modal Trigger Button -->
<button onclick="openModal('info-modal')">Open Info Modal</button>

<!-- Hidden Modal -->
<div class="modal" id="info-modal" style="display: none">
    <div class="modal-heading">
        Information
    </div>
    <div class="modal-body">
        <p>This modal can be opened by clicking the button above.</p>
        <p class="text-center">
            <button class="alt" onclick="closeModal()">Close</button>
        </p>
    </div>
</div>
```

### Closing Modals


Opened modal elements can be closed by invoking the JavaScript function, `closeModal()`.  This function can be easily attached to elements, like buttons.  For example:

```html
<button onclick="closeModal()"></button>
```

## Modal with Footer


You can add a footer section to your modal for action buttons:

Confirm Action
Are you sure you want to proceed with this action?
CancelDelete
```html
<div class="modal" id="confirm-modal" style="display: none">
    <div class="modal-heading">
        Confirm Action
    </div>
    <div class="modal-body">
        <p>Are you sure you want to proceed with this action?</p>
    </div>
    <div class="modal-footer">
        <button class="alt" onclick="closeModal()">Cancel</button>
        <button class="danger">Delete</button>
    </div>
</div>
```

## Form Inside Modal


Modals are perfect for containing forms:

Contact Form
Name
                    
                    
                    Email
                    
                    
                    Message
CancelSend
```html
<div class="modal" id="contact-modal" style="display: none">
    <div class="modal-heading">
        Contact Form
    </div>
    <div class="modal-body">
        <form>
            <label>Name</label>
            <input type="text" placeholder="Your name">
            
            <label>Email</label>
            <input type="email" placeholder="Your email">
            
            <label>Message</label>
            <textarea rows="3" placeholder="Your message"></textarea>
        </form>
    </div>
    <div class="modal-footer">
        <button class="alt" onclick="closeModal()">Cancel</button>
        <button>Send</button>
    </div>
</div>
```

## Close Modal Icons


It's also possible to add 'close modal' icons onto modals, producing a result that's similar to the kind of user experience that we may find on a native desktop application.

Example
**
On the top right hand side of this modal there is a small cross.  In a real-use situation, clicking the icon would have the effect of closing the modal.

Click the button below to see a working example of a modal that contains a 'close modal' icon:


Click Me!

Example Modal
**
On the top right hand side of this modal there is a small cross. Try clicking the icon and you'll notice that the modal window immediately closes.

In the example, the following CSS classes are being used to control the layout of the `.modal-header` element:


1. `.flex-row`
2. `.align-center`
3. `.justify-between`


Here's the source code:

```html
<div class="modal" id="close-icon-modal" style="display: none">
    <div class="modal-heading flex-row align-center justify-between">
        <div>Example Modal</div>
        <div><i class="fa fa-times" onclick="closeModal()"></i></div>
    </div>
    <div class="modal-body">
        <p class="text-left">On the top right hand side of this modal there is a small cross. Try clicking the icon and you'll notice that the modal window immediately closes.</p>
    </div>
</div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> In the example, we're using [Font Awesome](https://fontawesome.com/) to render a 'close modal' icon.   Font Awesome can be loaded onto your webpage by adding the following line of code onto the `<head>` section of your webpage:
> 
> ```html
> <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
> ```
> 
> 
> Don't forget to also add a CSS rule that turns the cursor into a pointer upon mouseover events!
> 
> ```css
> .modal-heading .fa {
>     cursor: pointer;
> }
> ```
> 
> 
> If you don't like using Font Awesome, you're free to use any other icon of your choosing.  You may wish to even consider rendering a 'close icon' using **pure HTML**. For example:
> 
> ```html
> <div onclick="closeModal()">&times;</div>
> ```


> [!TIP]
> **Best Practices**
>
> - Always provide a way to close the modal (close button or cancel option).
> - Keep modal content focused and concise.
> - Use appropriate modal sizes for different types of content.
> - Consider mobile responsiveness.
> - Use clear and descriptive heading text.
> - Ensure all modals have unique IDs.


## JavaScript Functions


Two main functions are available for modal control:


1. `openModal(modalId)`: Opens the modal with the specified ID
2. `closeModal()`: Closes the currently open modal


Example usage:

```html
<!-- Trigger buttons -->
<button onclick="openModal('example-modal')">Open Modal</button>
<button onclick="closeModal()">Close Modal</button>
```

### Loading The JavaScript Code


The JavaScript code for handling modals is contained within the following JavaScript files:


1. app.js
2. admin.js
3. trongate-mx.js


The JavaScript files are located in:

```
public/ 
  js/
```


All three of these files are provided with *every* installation of Trongate.

> [!NOTE]
> **Just To Let You Know...**
>
> You only have to load ***one*** of the above JavaScript files to enjoy full modal opening and closing functionality.


> [!TIP]
> **Best Practices**
>
> - If you're working with one of Trongate's pre-built admin panels, use **admin.js**.
> - If you're working with Trongate MX, use **trongate-mx.js**.
> - For all other situations, use **app.js**.
> 
> 
> **IMPORTANT NOTE: ** It's perfectly acceptable to load Trongate MX ('trongate-mx.js') onto a webpage that *already* uses either 'app.js' or 'admin.js'.



The following code demonstrates an example of basic HTML boilerplate required for implementing modal functionality with Trongate.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <base href="<?= BASE_URL ?>">
    <link rel="stylesheet" href="css/trongate.css">
    <title>Document</title>
</head>
<body>
    <h1>Ready!</h1>
    <script src="js/app.js"></script>
</body>
</html>
```

## Dynamic Modal Generation


**Trongate MX** pushes the boundaries of modern web development by providing a mechanism for generating modals entirely *dynamically*. This means that developers who'd like to have modal elements within their applications *no longer* have a requirement to hard-code hidden modal elements into their source code.


For example, if you click the button below, a modal will be dynamically generated. The contents of the modal will be extracted by fetching the headline element from the homepage of this website. Give it a try!

Open Dynamic Modal

To the untrained eye, the end result may look and behave like an ordinary modal. However, what's happening behind the scenes is remarkable. That's because the entire modal (both the contents and the modal window *itself*) are being generated and rendered dynamically.


Here's the source code:

```html
<button mx-get="/" mx-select="h1" mx-target=".modal-body"   
        mx-build-modal='{
            "id": "demo-headline-modal",
            "width": "640px",
            "modalHeading": "Dynamic Modal Demo",
            "showCloseButton": "true"
        }'>
    Open Dynamic Modal
</button>
```

> [!WARNING]
> To make the above example work, you'll have to [load Trongate MX](../../trongate_mx/0010Introduction/0020trongate_mx_quick_start.md) onto your webpage.


> [!TIP]
> **Best Practices**
>
> The example above is an attempt to introduce you to the general topic of dynamic modal generation.   Full instructions and guidance, pertaining to dynamic modal generation, is beyond the scope of the 'Trongate CSS' documentation.
> 
> 
> If dynamic modal generation and advanced front-end development, with Trongate, is something you'd like to learn more about, please refer to the [Trongate MX Documentation](../../trongate_mx/0050UI_Enhancements/0079building_dynamic_modals.md).


