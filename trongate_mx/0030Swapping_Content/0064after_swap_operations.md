# After Swap Operations


The `mx-after-swap` attribute in Trongate MX allows you to execute JavaScript functions immediately after content updates. It's a powerful feature that helps you create dynamic, interactive web applications.

## Usage


Here's a simple example showing how to use the `mx-after-swap` attribute:

```vf
<?php
$attributes = [
  'mx-get' => 'api/message',
  'mx-target' => '#message-area',
  'mx-after-swap' => 'showMessage'
];
echo form_button('update_btn', 'Get Message', $attributes);
?>

<div id="message-area"></div>

<script>
function showMessage(customEvent) {
  alert('Content updated successfully!');
}
</script>
```


The code above uses Trongate's form_button() function.  If you'd rather work directly with HTML, here's the code:

```html
<button mx-get="api/message"
        mx-target="showMessage"
        mx-after-swap="showMessage"></button>

<div id="message-area"></div>

<script>
function showMessage(customEvent) {
  alert('Content updated successfully!');
}
</script>
```


When the button is clicked, content is fetched from 'api/message' and placed into the message-area div. Once the content update is complete, a JavaScript function named `showMessage()` will be invoked.  The JavaScript function - in this instance - produces a simple alert message to confirm the successful update.

## More Examples

### Smooth Scroll After Update


Let's imagine you're viewing a page with lots of content, and you dynamically load new data into a specific section of the page. After the content updates, you may the page to scroll smoothly back to the top for better usability.


Here's how we can achieve this with Trongate MX:

```vf
<?php
$attributes = [
  'mx-get' => 'api/content',
  'mx-target' => '#content-area',
  'mx-after-swap' => 'scrollToTop'
];
echo form_button('scroll_btn', 'Load Content', $attributes);
?>

<div id="content-area"></div>

<script>
function scrollToTop(customEvent) {
  window.scrollTo({
      top: 0,
      behavior: 'smooth'
  });
}
</script>
```

> [!NOTE]
> **Just To Let You Know...**
>
> The `scrollToTop` function is a JavaScript function that scrolls the page smoothly to the top when called.



This example is particularly useful for long pages where new content is loaded by clicking a button that is further down the page. After the content update occurs, the page smoothly scrolls back to the top.


If you do not wish to use Trongate's form_button() function, you could produce the same results with the following code:

```html
<button mx-get="api/content"
        mx-target="#content-area"
        mx-after-swap="scrollToTop">Load Content</button>

<div id="content-area"></div>

<script>
function scrollToTop(customEvent) {
  window.scrollTo({
      top: 0,
      behavior: 'smooth'
  });
}
</script>
```

### Complex Update with Multiple Operations


You're not restricted to just performing just *one* task after elements have been swapped.  The code below demonstrates how to invoke several JavaScript functions after a successful element swap:

```vf
<?php
$attributes = [
  'mx-get' => 'api/dashboard',
  'mx-target' => '#dashboard',
  'mx-after-swap' => 'initDashboard'
];
echo form_button('dashboard_btn', 'Load Dashboard', $attributes);
?>

<div id="dashboard"></div>

<script>
function initDashboard(customEvent) {
  const dashboard = customEvent.detail.element;
  attachEventListeners(dashboard);
  initializeWidgets(dashboard);
  updateRelatedContent(dashboard);
  console.log('Dashboard loaded:', dashboard);
}
function attachEventListeners(dashboard) { /* ... */ }
function initializeWidgets(dashboard) { /* ... */ }
function updateRelatedContent(dashboard) { /* ... */ }
</script>
```


This more complex example demonstrates how to handle dashboard updates that require multiple initialization steps. After the dashboard content is loaded, the code sets up event listeners, initializes various widgets, and updates related content - all common requirements when working with dynamic dashboards.

> [!TIP]
> **Best Practices**
>
> - **Keep it Simple:** After-swap functions should be focused and perform clear tasks
> - **Use the Event Object:** Access swap information through the customEvent parameter
> - **Consider Timing:** These functions run immediately after content updates
> - **Ensure Availability:** Keep functions in global scope for Trongate MX to access them


## Summary


The `mx-after-swap` attribute provides a straightforward way to execute JavaScript after content updates. It accepts a single function name and passes a custom event object containing swap operation details. This enables you to create responsive applications where content updates and post-update processing work seamlessly together.

