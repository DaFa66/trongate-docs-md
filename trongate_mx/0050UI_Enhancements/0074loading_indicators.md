# Loading Indicators


Trongate MX makes it incredibly easy to add loading indicators to your web applications. These indicators give users clear feedback that something is happening behind the scenes, improving your application's professionalism and user experience.

## Quick Demonstration


Click the button below to see a loading indicator in action:

Fetch Data
## What Are Loading Indicators?


Loading indicators are temporary visual cues displayed while your application processes requests or fetches data. Trongate MX makes implementing these indicators simple and intuitive.

## Getting Started

### 1. Add a Spinner Element


Trongate comes with a built-in spinner. To create one, add a `<div>` element with the class `spinner`. For example:

```html
<div class="spinner"></div>
```


To make the spinner function as a loading indicator, add the `mx-indicator` class:

```html
<div class="spinner mx-indicator"></div>
```

### 2. Use the mx-indicator Attribute


Assign the `mx-indicator` attribute to the button (or any element) that triggers the HTTP request. The attribute value should match the CSS selector for your spinner element:

```html
<button mx-get="api/fetch_data" 
        mx-target="#result" 
        mx-indicator=".spinner">Fetch Data</button>
```


Here's a complete example, using Trongate's form_button() function:

```vf
<?php
$btn_attr = [
  'mx-get' => 'api/fetch_data',
  'mx-target' => '#result',
  'mx-indicator' => '.spinner'
];
echo form_button('fetch_btn', 'Fetch Data', $btn_attr);
?>

<div class="spinner mx-indicator"></div>
<div id="result"></div>
```


For an HTML-only approach, here's the corresponding code:

```html
<button mx-get="api/fetch_data" 
        mx-target="#result" 
        mx-indicator=".spinner">Fetch Data</button>

<div class="spinner mx-indicator"></div>
<div id="result"></div>
```

> [!TIP]
> **Best Practices**
>
> During development, use PHP's `sleep()` function to introduce a delay in your API responses. This gives you time to see how your indicators work:
> 
> ```php
> public function fetch_data() {
>     sleep(2);
>     echo 'Hello from the API!';
> }
> ```


> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** The `spinner` class is part of the Trongate CSS library. It works straight out of the box without additional styles or JavaScript.


## Custom Loading Indicators


You're not limited to the default spinner. You can create custom indicators using any HTML element:

```html
<div id="custom-loader" class="mx-indicator">
  <p class="blink">Saving your changes...</p>
  <img src="images/custom-loader.gif" alt="Loading...">
</div>
```


Here's an example of using a custom loading indicator in a form:

```vf
<?php
$form_attr = [
  'mx-post' => 'api/submit_form',
  'mx-target' => '#response',
  'mx-indicator' => '#custom-loader'
];
echo form_open('#', $form_attr);
echo form_submit('submit', 'Save Changes');
echo form_close();
?>

<div id="custom-loader" class="mx-indicator">
  <p class="blink">Saving your changes...</p>
  <img src="images/custom-loader.gif" alt="Loading...">
</div>

<div id="response"></div>
```


For an HTML-only approach, here's an alternative syntax:

```html
<form mx-post="api/submit_form"
      mx-target="#response"
      mx-indicator="#custom-loader">
    <button type="submit">Save Changes</button>
</form>

<div id="custom-loader" class="mx-indicator">
  <p class="blink">Saving your changes...</p>
  <img src="images/custom-loader.gif" alt="Loading...">
</div>

<div id="response"></div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> The class `blink` in Trongate CSS creates a smooth, fading animation that makes the text blink.


## Advanced Usage: Multiple Indicators


Need different indicators for different areas of your page? No problem! Assign unique `mx-indicator` attributes to each button:

```vf
<?php
// Button for user data
$user_btn = [
  'mx-get' => 'users/fetch_details',
  'mx-target' => '#user-data',
  'mx-indicator' => '#user-loader'
];
echo form_button('user_btn', 'Load User Data', $user_btn);

// Button for order data
$order_btn = [
  'mx-get' => 'orders/fetch_recent',
  'mx-target' => '#order-data',
  'mx-indicator' => '#order-loader'
];
echo form_button('order_btn', 'Load Orders', $order_btn);
?>

<div id="user-loader" class="spinner mx-indicator"></div>
<div id="user-data"></div>

<div id="order-loader" class="spinner mx-indicator"></div>
<div id="order-data"></div>
```


Here's how the solution looks when written entirely in HTML:

```html
<button mx-get="users/fetch_details"
        mx-target="#user-data"
        mx-indicator="#user-loader">Load User Data</button>

<button mx-get="orders/fetch_recent"
        mx-target="#order-data"
        mx-indicator="#order-loader">Load Orders</button>

<div id="user-loader" class="spinner mx-indicator"></div>
<div id="user-data"></div>

<div id="order-loader" class="spinner mx-indicator"></div>
<div id="order-data"></div>
```

## Summary


Loading indicators are an essential part of any modern web application. With Trongate MX, implementing them is simple, intuitive, and requires no JavaScript. Whether you use the built-in spinner or create custom indicators, you can deliver a polished and professional experience to your users.

