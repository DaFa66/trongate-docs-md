# On Trigger Operations


The `mx-on-trigger` attribute in Trongate MX allows you to execute your own custom JavaScript functions 
  immediately after a trigger event occurs, but **before** any HTTP request is made. This enables you to 
  perform actions like showing messages, manipulating the page, or performing checks before a request begins.

## Basic Usage


The `mx-on-trigger` attribute works alongside other Trongate MX attributes like 
  `mx-get` or `mx-post`. It executes your specified JavaScript function 
  when the trigger event (like a click) happens, but before any HTTP request is invoked by Trongate MX.


---

### Simple Example:


In the following example, when the button is clicked, the user sees a "Hello" pop-up alert *before* the 
  system fetches data from the target URL.

```vf
<?php
$btn_attr = [
  'mx-get' => 'api/data',
  'mx-target' => '#result',
  'mx-on-trigger' => 'sayHello'
];
echo form_button('load_data_btn', 'Load Data', $btn_attr);
?>

<div id="result"></div>

<script>
function sayHello() {
  alert('Hello! Getting your data now...');
}
</script>
```


Here's how the code looks when written entirely in HTML:

```html
<button mx-get="api/data" 
        mx-target="#result" 
        mx-on-trigger="sayHello">Load Data</button>

<div id="result"></div>

<script>
function sayHello() {
  alert('Hello! Getting your data now...');
}
</script>
```

> [!NOTE]
> **Just To Let You Know...**
>
> As a reminder, there's no obligation to use Trongate's form helpers when working with Trongate MX.
> 
> 
> This means that you can use Trongate form helpers (like form_button()) or, alternatively, you can work with pure HTML.


## Passing Event Information Into Functions


Functions invoked by `mx-on-trigger` automatically receive event information related to the trigger. 
  This allows for greater flexibility, such as dynamically interacting with the clicked element.

### Example Of Automatic Event Handling

```vf
<?php
$btn_attr = [
  'mx-get' => 'api/data',
  'mx-target' => '#result',
  'mx-on-trigger' => 'buildCustomSpinner'
];
echo form_button('fetch_data_btn', 'Load Data', $btn_attr);
?>
```


In this example, the JavaScript function `buildCustomSpinner` gets invoked the moment after the form button is clicked (and before a response has been received from any API endpoint!).  The following JavaScript code could be used to test this basic functionality.

```javascript
function buildCustomSpinner(ev) {
  const clickedEl = ev.target;
  alert(clickedEl.outerHTML);
}
```

### Practical Example Using Event Information


Here's a more practical implementation where the triggering button is disabled and a loading class is added:

```javascript
function buildCustomSpinner(ev) {
  // Get the clicked button
  const clickedBtn = ev.target;

  // Disable the button to prevent double-clicks
  clickedBtn.disabled = true;

  // Add a loading class
  clickedBtn.classList.add('loading');
}
```

## More Examples

### 1. Scroll to Top Before Loading


This example shows how to smoothly scroll the page back to the top before loading new content into a target element.

```vf
<?php
$btn_attr = [
  'mx-get' => 'api/data',
  'mx-target' => '#content',
  'mx-on-trigger' => 'scrollToTop'
];
echo form_button('load_btn', 'Load New Content', $btn_attr);
?>

<div id="content"></div>

<script>
function scrollToTop() {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  });
}
</script>
```


Here's an alternative syntax for developers who prefer to work with pure HTML:

```html
<button mx-get="api/data" 
        mx-target="#content" 
        mx-on-trigger="scrollToTop">Load New Content</button>

<div id="content"></div>

<script>
function scrollToTop() {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  });
}
</script>
```


---

### 2. Simple Confirmation Check


This example demonstrates how to implement a confirmation dialog before proceeding with a checkout process, preventing the HTTP request if the user cancels.

```vf
<?php
$btn_attr = [
  'mx-post' => 'api/checkout',
  'mx-target' => '#checkout-status',
  'mx-on-trigger' => 'confirmCheckout'
];
echo form_button('buy_btn', 'Complete Purchase', $btn_attr);
?>

<div id="checkout-status"></div>

<script>
function confirmCheckout() {
  const userConfirmed = confirm('Ready to complete your purchase?');
  if (!userConfirmed) {
    throw new Error('Checkout cancelled');
  }
}
</script>
```


Here's how the code looks when written *without* using any of Trongate's form helper functions:

```html
<button mx-post="api/checkout" 
        mx-target="#checkout-status" 
        mx-on-trigger="confirmCheckout">Complete Purchase</button>

<div id="checkout-status"></div>

<script>
function confirmCheckout() {
  const userConfirmed = confirm('Ready to complete your purchase?');
  if (!userConfirmed) {
    throw new Error('Checkout cancelled');
  }
}
</script>
```


---

## Advanced Usage: Async Functions

### 3. Async Inventory Check Example


This example demonstrates how to use an async function to check inventory status before proceeding with a submission, preventing the request if the item is out of stock.

```vf
<?php
$btn_attr = [
  'mx-post' => 'api/purchase',
  'mx-target' => '#purchase-status',
  'mx-on-trigger' => 'checkBeforeSubmit'
];
echo form_button('purchase_btn', 'Purchase Item', $btn_attr);
?>

<div id="purchase-status"></div>

<script>
async function checkBeforeSubmit() {
    try {
        const result = await checkInventory();
        if (!result.inStock) {
            alert('Item not in stock!');
            throw new Error('Not in stock');
        }
    } catch (error) {
        throw error;
    }
}
</script>
```


Here's an alternative syntax for those who prefer to work with pure HTML:

```html
<button mx-post="api/purchase" 
        mx-target="#purchase-status" 
        mx-on-trigger="checkBeforeSubmit">Purchase Item</button>

<div id="purchase-status"></div>

<script>
async function checkBeforeSubmit() {
    try {
        const result = await checkInventory();
        if (!result.inStock) {
            alert('Item not in stock!');
            throw new Error('Not in stock');
        }
    } catch (error) {
        throw error;
    }
}
</script>
```

> [!TIP]
> **Best Practices**
>
> If you're not familiar with async/await, stick to regular functions like in the earlier 
>     examples - they'll work fine for most use cases!


## Summary


The `mx-on-trigger` attribute provides a way to run custom JavaScript code ***before* Trongate MX 
    invokes HTTP requests**. You can use it for simple tasks like showing messages or scrolling the page, 
    or for more complex tasks like validation. The event object is automatically passed to your functions, 
    giving you access to information about the triggering element. By throwing errors in your functions, 
    you can prevent requests from proceeding when needed.

