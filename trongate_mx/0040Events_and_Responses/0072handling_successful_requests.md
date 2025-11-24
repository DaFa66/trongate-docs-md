# Handling Successful Requests


The `mx-on-success` attribute lets you trigger elements after an HTTP request has been made and a response code within the success range has been received.  This makes it possible for one action (such as the submission of a form) to result in several different parts of a page being updated.

> [!WARNING]
> **Warning!**
>
> The `mx-on-success` attribute (which happens to be the focus of this page) is designed for reinitialising elements, **not** for executing custom JavaScript!
> 
> 
> To execute your own custom JavaScript code after an HTTP request, use the `mx-after-swap` attribute. You can find the relevant documentation [here](documentation/display/trongate_mx/swapping-content/after-swap-operations).


## Syntax


When working with `mx-on-success`, we should assign a CSS selector value to indicate which 
  element should be updated (i.e., **triggered**) after a successful request.

```vf
<element mx-on-success="#target-element">
```

## How It Works


When Trongate MX completes an AJAX request successfully, here's what happens:


1. Trongate MX checks the element (that invoked the HTTP request) for an `mx-on-success` attribute.
2. If an `mx-on-success` attribute is found, the value that has been assigned to the attribute is read.
3. Trongate MX identifies an element whose CSS selector matches the value of `mx-on-success`.
4. Any [HTTP requests  tied to the target element](documentation/display/trongate_mx/core-http-operations/http-methods-in-trongate-mx) are triggered, reinitialising it.


This makes it easy to refresh multiple, dynamic sections of your application or set up chained actions.

> [!NOTE]
> **Just To Let You Know...**
>
> Throughout this documentation, you'll see phrases like:
> 
> 
> - "receives a response within the 'success' range"
> - "completes an AJAX request successfully"
> 
> 
> Whenever you see phrases like that, it's usually a reference to the **HTTP response status code** that has been received from an API endpoint.
> 
> 
> **Success Range (2xx)**
> 
> 
> HTTP response status codes within the range of **200-299** indicate that the request was successful.
> 
> 
> Common examples include:
> 
> 
> - 200 OK: Request was successful and data is returned.
> - 201 Created: A new resource has been created.
> - 204 No Content: Request was successful but no content is returned.


## Example


In the following example, we have a form that submits a POST request to an API endpoint.


When a response is received from the server that has an HTTP response status code within the success range, a `<div>` element with an "id" of "order-summary" is triggered.


Since the targetted element has an `mx-get` attribute, a second HTTP request will immediately be made. Specifically, this will be a GET request to the target URL of 'api/get_order_summary'.

```vf
<?php
$form_attr = [
    'mx-post' => 'api/submit_order',
    'mx-target' => '#order-confirmation',
    'mx-on-success' => '#order-summary'
];
echo form_open('#', $form_attr);
echo form_submit('submit', 'Place Order');
echo form_close();
?>
<div id="order-confirmation"></div>
<div id="order-summary" mx-get="api/get_order_summary" mx-trigger="load">
  <!-- Order summary content -->
</div>
```


Since the usage of Trongate's form helper functions is optional, here's an alternative syntax that uses pure HTML:

```html
<form mx-post="api/submit_order"
      mx-target="#order-confirmation"
      mx-on-success="#order-summary">

    <button type="submit">Place Order</button>
</form>

<div id="order-confirmation"></div>
<div id="order-summary" mx-get="api/get_order_summary" mx-trigger="load">
  <!-- Order summary content -->
</div>
```

## Understanding The Code


The example above demonstrates a common code pattern.  It's therefore worth taking a few moments to understand how it works.  Don't worry if the example above seems overwhelming at first.  It'll become clearer with patience and a little practice!

### So, what's the point?


To be clear, the goal we're trying to achieve - with this code - is as follows:


**We're trying to update multiple different parts of a page after an HTTP request - made by Trongate MX - has been successfully completed.**


---

### Why does this matter?


Having the ability to update *multiple* different parts of a page, without refreshing the entire page allows us to build extremely powerful applications.  It's the kind of advanced functionality that we might expect to find on [sophisticated admin panels](https://wrapbootstrap.com/category/templates/admin-templates) that get used in business.


---

### Do we really need Trongate MX for this?


Of course we don't!  However, without Trongate MX you'd have to either:


1. Writes lots of custom JavaScript code.
2. Refresh the entire page every time an update happens.
3. Use a JavaScript framework that might get rewritten tomorrow!


Surely you'll agree, none of those three options are ideal - particularly if you're trying to build a modern application quickly and with massive degrees of stability.

> [!NOTE]
> **Just To Let You Know...**
>
> By the way, if you're still not sold on Trongate MX - just imagine a stock market trading website where you had to manually refresh the entire page every time a stock price changed.  Such an application would be considered to be hopelessly old-fashioned and perhaps even useless!
> 
> 
> This is why Trongate MX is a really important tool for the Trongate ecosystem.  It lets you build modern web applications quickly and easily.


### How does the code example above work?


The best way to understand the code example, shown above, is to start from the bottom and work our way up. So, let's consider this element:

```html
<div id="order-summary" mx-get="api/get_order_summary" mx-trigger="load">
  <!-- Order summary content -->
</div>
```


The element above is an empty div with an id of 'order-summary'. If you look closely, you'll see that the div contains an attribute of `mx-trigger` with a value of '**load**'. From this, we know that the element is going to be triggered the moment the page has finished loading.


Have a closer look and you'll notice that the '#order-summary' div also has an `mx-get` attribute with a value of 'api/get_order_summary'.


From this, we now know that as soon as the page loads, a GET request will be made and (if all goes well!) order details will be added inside the '#order-summary' element.

> [!TIP]
> **Best Practices**
>
> If the behaviour of the #order-summary element is confusing, you are encouraged to refer to our section on [Triggers In Trongate MX](documentation/display/trongate_mx/events-and-responses/triggers-in-trongate-mx).



Moving up, we see another div element:

```html
<div id="order-confirmation"></div>
```


This empty div with an id of 'order-confirmation' will be used to display the response from our form submission. Notice that it doesn't have any Trongate MX attributes of its own - it's simply a target for our server response.


You may wonder,


"What *is* the server response going to be?"


Good question!


Well... it could be something as simple as some text containing the words,

`The order was successfully updated.`
It's no big deal and perhaps *not* as complicated as you may have assumed!

### The Form Structure


Now let's examine the form, in our example:

```php
$form_attr = [
    'mx-post' => 'api/submit_order',
    'mx-target' => '#order-confirmation',
    'mx-on-success' => '#order-summary'
];
echo form_open('#', $form_attr);
```


This form has three important Trongate MX attributes:


1. `mx-post`: When the form is submitted, it will make a POST request to 'api/submit_order'.
2. `mx-target`: The response from this POST request will be displayed in the '#order-confirmation' div.
3. `mx-on-success`: If the POST request is successful (returns a 2xx status code), the '#order-summary' div will be triggered.

### The Complete Flow


Now that we understand each piece, here's how it all works together:


1. When the page first loads, the '#order-summary' div is automatically triggered (due to `mx-trigger="load"`), making a GET request to fetch and display the initial order summary.
2. When a user clicks the "Place Order" button, the form submits a POST request to 'api/submit_order'.
3. The response from this POST request is displayed in the '#order-confirmation' div.
4. If the POST request was successful, the '#order-summary' div is triggered again.
5. This trigger causes another GET request to 'api/get_order_summary', refreshing the order summary with the latest data.

## Why This Pattern Is Useful


This pattern is particularly helpful when you need to update multiple elements after a successful form submission. The initial form submission can return a success message, while the triggered element can fetch and display updated data without requiring a full page reload.

> [!NOTE]
> **Just To Let You Know...**
>
> If you look closely at the code example above, you might notice a hash ('#') symbol being passed into the form_open() function as an argument. This might seem unusual since the first argument is typically expected to be the target URL where the form will post.
> 
> 
> The hash symbol is used here because the `mx-post` attribute overrides any 'action' or 'method' properties that would normally be found in a standard form opening tag.


## Working With Pure HTML


As a reminder, you're not obligated to use Trongate's form helper functions when working with Trongate MX. If you prefer to work with pure HTML, the following code could be used:

```html
<form mx-post="api/submit_order" 
      mx-target="#order-confirmation" 
      mx-on-success="#order-summary"> 
    <button type="submit">Place Order</button> 
</form>

<div id="order-confirmation"></div>

<div id="order-summary" mx-get="api/get_order_summary" 
                        mx-trigger="load"></div>
```

## Things to Keep in Mind


- `mx-on-success` only works for client-side handling of successful AJAX requests.
- It won't affect elements during the initial page load.

