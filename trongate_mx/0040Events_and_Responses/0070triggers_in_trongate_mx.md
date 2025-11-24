# Triggers in Trongate MX


The `mx-trigger` attribute in Trongate MX allows you to specify events that trigger HTTP requests. This powerful feature enhances the interactivity and responsiveness of your web application by defining when and how requests should be initiated.

## Usage


Set the `mx-trigger` attribute on an element to control the event that triggers the request. If not specified, Trongate MX uses default events based on the element type.

### Basic Example:


In the following example, the HTTP GET request is triggered when the button is clicked.

```vf
<?php
$attributes = [
  'mx-get' => 'api/data',
  'mx-trigger' => 'click'
];

echo form_button('fetch_btn', 'Get Data', $attributes);
?>
```


For those who prefer to work with pure HTML, here's an alternative way to write the code:

```html
<button mx-get="api/data" mx-trigger="click">Get Data</button>
```

> [!NOTE]
> **Just To Let You Know...**
>
> In the example above, there is - strictly speaking - no need to declare an `mx-trigger` attribute with a value of 'click'. This is because button elements are automatically assigned click events as their default triggers by Trongate MX. In other words, even if we did *not* specify an `mx-trigger` value of 'click' on the button, it would *still* behave as if the `mx-trigger` had been set to 'click'.
> 
> 
> This means that the following code would have produced the same result as the two code snippets shown above:
> 
> ```html
> <button mx-get="api/data">Get Data</button>
> ```


## Default Trigger Events


When the `mx-trigger` attribute is not provided, Trongate MX determines the natural trigger event based on the element type.  The following table shows the default trigger events for different HTML elements:


| Element Type | Default Trigger Event |
| ---|---|
| form | submit |
| button | click |
| input (type="submit") | click |
| input (other types) | change |
| textarea | change |
| select | change |
| other elements | click |

## Supported Events


Trongate MX listens for various events and triggers the appropriate HTTP requests based on the `mx-trigger` attribute:


- click
- dblclick
- change
- submit
- keyup
- keydown
- focus
- blur
- activate (special value for programmatic triggers only)

## Load Event


The `load` event is a special case that triggers the request when the page is loaded:

```html
<div mx-get="api/initial-data" mx-trigger="load"></div>
```


This will fetch data from the API as soon as the page loads.

> [!TIP]
> **Best Practices**
>
> - **Use specific events**: Specify the exact event that should trigger the request to avoid unintended behavior.
> - **Combine with other attributes**: Use `mx-trigger` in conjunction with other Trongate MX attributes like `mx-get`, `mx-post`, and `mx-target` for more complex interactions.
> - **Consider performance**: Be mindful of the frequency of triggered events to avoid excessive server load and client-side performance issues.
> - **Error handling**: Implement appropriate error handling for failed requests to ensure a smooth user experience.


## Programmatic Activation


The special value of '`activate`' can be used to specify that an element should only respond to programmatic triggers (e.g., from `mx-on-success` or `mx-on-error`) rather than user events:

> [!NOTE]
> **Just To Let You Know...**
>
> Using `mx-trigger="activate"` serves a specific purpose. When you add this attribute to an element, it prevents that element from responding to any user events (like clicks or changes) while still allowing it to be triggered programmatically through `mx-on-success` or `mx-on-error`. Without this attribute, the element would respond to both user events AND programmatic triggers, which might not be what you want.
> 
> 
> Think of `mx-trigger="activate"` as a way of saying "this element should respond to programmatic triggers, never to default trigger events."


```vf
<!-- This table will only refresh when triggered by mx-on-success -->
<table class="data-table" 
       mx-get="api/get_data" 
       mx-trigger="activate">
    <!-- table content -->
</table>

<!-- This button triggers the table refresh on success -->
<?php
$btn_attr = [
  'mx-post' => 'api/update_data',
  'mx-on-success' => '.data-table'
];
echo form_button('update_btn', 'Update Data', $btn_attr);
?>
```


In this example, the table won't respond to user clicks or other events, but will refresh when the button's POST request succeeds.

> [!NOTE]
> **Just To Let You Know...**
>
> When you add an `mx-trigger` attribute to an element, all default triggers that would otherwise be associated with the element are disabled. For example, if you add `mx-trigger="load"` to a button, it will no longer respond to clicks (which would normally be the default for buttons).
> 
> 
> Note that elements can still be triggered programmatically through `mx-on-success` or `mx-on-error` attributes on other elements, regardless of their `mx-trigger` value.



For an HTML-only approach, here's the corresponding code:

```html
<!-- This table will only refresh when triggered by mx-on-success -->
<table class="data-table" 
       mx-get="api/get_data" 
       mx-trigger="activate">
    <!-- table content -->
</table>

<!-- This button triggers the table refresh on success -->
<button mx-post="api/update_data" 
        mx-on-success=".data-table">Update Data</button>
```

> [!NOTE]
> **Just To Let You Know...**
>
> Documentation covering the `mx-on-success` attribute is available [from here](documentation/display/trongate_mx/events-and-responses/handling-successful-requests).
> 
> 
> Documentation covering the `mx-on-error` attribute is available [from here](documentation/display/trongate_mx/events-and-responses/handling-request-errors).


## Disabling Triggers


There may be cases where you want an element to have attributes like `mx-get` without responding to any user events, allowing you to invoke the request only programmatically. Setting `mx-trigger="none"` provides a simple way to accomplish this:

```html
<div id="data-container" 
     mx-get="api/fetch_data" 
     mx-trigger="none">
  <!-- This element won't respond to clicks or other user events -->
</div>

<script>
function fetchDataProgrammatically() {
  // Manually fetch using the Trongate MX API
  const container = document.querySelector('#data-container');
  window.TrongateMX.fetch(container); // Trigger the request programmatically
}
</script>
```


This approach is particularly useful in these scenarios:


1. **Elements with polling**: When you want to [control polling programmatically](documentation/display/trongate_mx/advanced-features/polling-with-trongate-mx) without having the element respond to user clicks
2. **Hidden elements**: For elements that contain API configuration but shouldn't trigger requests when clicked
3. **Containers with complex content**: For containers that have clickable children but shouldn't trigger requests when the container itself is clicked


Unlike `mx-trigger="activate"` which still allows programmatic activation via `mx-on-success` or `mx-on-error`, `mx-trigger="none"` completely disables automatic triggering, giving you full control over when the request occurs.

## Summary


By leveraging the `mx-trigger` attribute, you can create more dynamic and responsive web applications with Trongate MX, allowing for sophisticated event-driven interactions with minimal JavaScript code.

