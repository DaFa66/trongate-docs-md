# Trongate MX Quick Start Guide


This guide will help you quickly get started with Trongate MX. Please ensure you have the latest version of Trongate installed before proceeding.

## Step 1: Include Required Files


Trongate MX requires two main files to function properly:


1. The JavaScript file "**trongate-mx.js**" located in:

```
public/ 
  js/ 
    trongate-mx.js
```


2. The CSS stylesheet "**trongate.css**" located in:

```
public/ 
  css/ 
    trongate.css
```


To activate these files, add the following lines to your website template:

```html
<!-- Include Trongate CSS in the <head> section -->
<link rel="stylesheet" href="<?= BASE_URL ?>css/trongate.css">

<!-- Include Trongate MX JavaScript -->
<script src="<?= BASE_URL ?>js/trongate-mx.js"></script>
```


The JavaScript file can be placed either:


- In the `<head>` section of your HTML document, or 
- Just before the closing `</body>` tag 


Both placements are valid because Trongate MX initializes after the page loads. The choice of placement can depend on your specific needs and preferences for page loading behaviour. However, the CSS stylesheet should always be included in the `<head>` section.

> [!TIP]
> **Best Practices**
>
> It's highly recommended to include a `<base>` tag in the head section of any webpage that uses Trongate MX. For example:
> 
> ```html
> <base href="<?= BASE_URL ?>">
> ```
> 
> 
> Adding this to the head section of your page offers several benefits:
> 
> 
> - It simplifies your URLs, resulting in less typing.
> - It makes your code cleaner and more maintainable.
> - It allows for easier migration or changing of your base URL in the future.
> 
> 
> With the `<base>` tag, instead of writing:
> 
> ```html
> <link rel="stylesheet" href="<?= BASE_URL ?>css/trongate.css">
> <script src="<?= BASE_URL ?>js/trongate-mx.js"></script>
> ```
> 
> 
> You can simply write:
> 
> ```html
> <link rel="stylesheet" href="css/trongate.css">
> <script src="js/trongate-mx.js"></script>
> ```


## Step 2: Create an API Endpoint


Before using Trongate MX to make API calls, you'll need to create an endpoint in your controller. Here's an example of a simple API endpoint that returns HTML:

```php
<?php
class Welcome extends Trongate {

    function get_message() {
        echo '<h3>Hello from the API!</h3>';
        echo '<p>This is <b>pure HTML</b> being returned from the server.</p>';
        echo '<p>The time is: '.date('H:i:s').'</p>';
    }

}
```


Notice how this endpoint returns pure HTML instead of JSON. This is one of the powerful features of Trongate MX!

## Step 3: Invoke AJAX Requests without Writing Any JavaScript!


The code below invokes an HTTP request.  Notice that it's just pure HTML with a couple of 'mx' attributes added.

```html
<button mx-get="welcome/get_message" 
        mx-target="#message-target">Click Me</button>

<div id="message-target"></div>
```


Here's the solution written using Trongate's form_button() form helper:

```vf
<?php
$btn_attr = [
    'mx-get' => 'welcome/get_message',
    'mx-target' => '#message-target'
];
echo form_button('fetch_btn', 'Click Me', $btn_attr);
?>

<div id="message-target"></div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> When using Trongate MX, you can take advantage of Trongate's form helper functions. However, if you prefer writing the syntax as pure HTML with 'mx' attributes, that's perfectly fine too.



In the above example, when clicked, the button will:


- Make an AJAX request to your API endpoint
- Handle the response
- Insert the returned HTML into the target element


The key components are:


- `mx-get="welcome/get_message"` specifies the API endpoint to call
- `mx-target="#message-target"` indicates where the response should be displayed


Congratulations! You've just taken your first step with Trongate MX. Unlike traditional approaches that force you to work with JSON and complex JavaScript code, Trongate MX lets you enjoy all the benefits of JavaScript but *without* having to actually *write* any JavaScript at all!  Best of all, you can return **pure HTML** directly from your endpoints. This means faster development, cleaner code and smashed deadlines!

