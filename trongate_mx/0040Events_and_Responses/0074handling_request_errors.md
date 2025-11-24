# Handling Request Errors


The `mx-on-error` attribute in Trongate MX lets you specify which elements should 
  update or reinitialise when an AJAX request fails. It offers a means of handling errors 
  gracefully and keeping your users informed when things don't go quite as planned.

> [!WARNING]
> **Warning!**
>
> The `mx-on-error` attribute (which happens to be the focus of this page) is designed for triggering elements, **not** for executing custom JavaScript!
> 
> 
> To execute your own custom JavaScript code after an HTTP request, use the `mx-after-swap` attribute. You can find the relevant documentation [here](documentation/display/trongate_mx/swapping-content/after-swap-operations).


## Syntax

```vf
<element mx-on-error="#error-element">
```


Use a CSS selector as the value of `mx-on-error`. This tells Trongate MX which 
  element should be updated or reinitialised after a request fails.

## How It Works


When Trongate MX encounters a failed AJAX request, here's what happens:


1. It checks if the triggering element has an `mx-on-error` attribute.
2. If it does, the framework finds the target element using your CSS selector.
3. Page load events tied to the target element are triggered, reinitialising it.


This makes it easy to display error messages or trigger fallback options when things go wrong.

## Example


The code sample below demonstrates a form that posts data to an API endpoint.  When something goes wrong, an error message is fetched from the url `api/get_error_details` and the message is displayed within a `<div>` that has an id of 'error-message'.

```html
<form mx-post="api/submit_data"
      mx-target="#result-container"
      mx-on-error="#error-message">
  <button type="submit">Submit Data</button>
</form>

<div id="result-container"></div>

<div id="error-message" mx-get="api/get_error_details"
                        mx-trigger="activate"></div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> Usually, if a form is submitted - and something goes wrong - it'll be appropriate to display [form validation errors](documentation/display/trongate_mx/form-handling/form-validation-and-error-handling). **That's not what's happening here!**
> 
> 
> In our example, the assumption is that we have a more sophistated error message to display when things go wrong.  For example, let's imagine a user is enrolling to join a course.  Let's further assume that - at the last moment - somebody else has enrolled and there are no more spaces left!
> 
> 
> As complicated as it may seem, this is *precisely* the kind of situation where a more sophisticated error message would be appropriate (as opposed to just a form validation error).
> 
> 
> In the error message, we might explain that there are no more spaces left and we may wish to give the user an opportunity to join a waiting list so that they can be kept informed of future courses or even cancellations.
> 
> 
> For information on how to render form validation errors with Trongate MX, [click here](documentation/display/trongate_mx/form-handling/form-validation-and-error-handling).



The code sample above uses pure HTML.  Below is a [more secure](documentation/display/trongate_mx/trongate-mx-security/csrf-protection)  solution that uses Trongate's form helper functions:

```vf
<?php
$form_attr = [
    'mx-post' => 'api/submit_data',
    'mx-target' => '#result-container',
    'mx-on-error' => '#error-message'
];
echo form_open('#', $form_attr);
echo form_submit('submit', 'Submit Data');
echo form_close();
?>

<div id="result-container"></div>

<div id="error-message" mx-get="api/get_error_details"
                        mx-trigger="activate"></div>
</div>
```


**What's Happening?**


1. If the form submission fails, the `mx-on-error="#error-message"` attribute kicks in.
2. This triggers the `#error-message` element.
3. Since `#error-message` has `mx-get` and `mx-trigger="activate"`, it fetches and displays the error details.

> [!NOTE]
> **Just To Let You Know...**
>
> You might notice we're using a hash ('#') symbol in the form_open() function. This is because the `mx-post` attribute takes care of the form's destination and method.


> [!TIP]
> **Best Practices**
>
> Consider using in combination with `mx-trigger="activate"`.  Without this attribute, the element may respond to both user events AND programmatic triggers, which might not be what you want.  For more information on this topic, refer to our documentation on [Triggers in Trongate MX](documentation/display/trongate_mx/events-and-responses/triggers-in-trongate-mx).


## Error Handling with Out-of-Band Swaps


When using `mx-target="none"` with out-of-band swaps, you can still utilize `mx-on-error` to handle request failures gracefully.

```html
<div id="dashboard-container" 
     mx-get="api/dashboard_data" 
     mx-target="none" 
     mx-select-oob='[
         {"select": ".visitors-data", "target": "#visitors-panel"},
         {"select": ".revenue-data", "target": "#revenue-panel"}
     ]'
     mx-on-error="#dashboard-error">
    
    <!-- Panels to be updated via OOB swaps -->
    <div id="visitors-panel"></div>
    <div id="revenue-panel"></div>
    
    <!-- Error message container (initially hidden) -->
    <div id="dashboard-error" style="display: none;" 
         mx-get="api/error_message" 
         mx-trigger="activate"></div>
</div>
```


In this example, if the request to `api/dashboard_data` fails, the `#dashboard-error` element will be activated. It will then fetch an error message from `api/error_message` and display it to the user.


This pattern is particularly useful for real-time dashboards and polling scenarios where you need to gracefully handle intermittent API failures without disrupting the entire user interface.

## Things to Keep in Mind


- `mx-on-error` only works for client-side handling of failed AJAX requests.
- It won't affect elements during the initial page load.
- You can target multiple elements by separating selectors with spaces (e.g., "#error-message #status-panel #notification-area").

