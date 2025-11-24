# Triggering Multiple Elements


The [previous page](documentation/display/trongate_mx/events-and-responses/handling-successful-requests) covered how to update/trigger **one element** after a successful HTTP request has been made.   This was achieved by using the `mx-on-success` attribute.


With `mx-on-success` it's also possible to trigger *multiple* elements by separating their selectors with spaces. Here's an example:

```vf
$form_attr = [
    'mx-post' => 'api/submit_order',
    'mx-target' => '#order-confirmation',
    'mx-on-success' => '#order-summary #customer-balance #recent-orders'
];
echo form_open('#', $form_attr);
echo form_submit('submit', 'Place Order');
echo form_close();
?>

<div id="order-confirmation"></div>

<div id="order-summary" mx-get="api/get_order_summary" mx-trigger="activate">
    <!-- Order summary content -->
</div>

<div id="customer-balance" mx-get="api/get_balance" mx-trigger="activate">
    <!-- Customer balance content -->
</div>

<div id="recent-orders" mx-get="api/get_recent_orders" mx-trigger="activate">
    <!-- Recent orders content -->
</div>
```


For those who prefer to work with pure HTML, here's an alternative syntax that produces the same result:

```vf
<form mx-post="api/submit_order"
        mx-target="#order-confirmation"
        mx-on-success="#order-summary #customer-balance #recent-orders">
    <button type="submit">Place Order</button>           
</form>

<div id="order-confirmation"></div>

<div id="order-summary" mx-get="api/get_order_summary" mx-trigger="activate">
    <!-- Order summary content -->
</div>

<div id="customer-balance" mx-get="api/get_balance" mx-trigger="activate">
    <!-- Customer balance content -->
</div>

<div id="recent-orders" mx-get="api/get_recent_orders" mx-trigger="activate">
    <!-- Recent orders content -->
</div>
```

> [!TIP]
> **Best Practices**
>
> You may have noticed that in the examples shown, the elements to be [triggered](documentation/display/trongate_mx/events-and-responses/triggers-in-trongate-mx)  have all been given the attribute, `mx-trigger="activate"`.
> 
> 
> The reason for this is to prevent default trigger behaviour from activating the target elements. By adding `mx-trigger="activate"`, we are effectively saying, "This element should *only* be activated when it is programmatically triggered by another element."
> 
> 
> If we did *not* include `mx-trigger="activate"` on the elements, they could potentially be triggered by clicks, which is - of course - not desirable.


### Understanding The Code


In this example, when the form submission is successful:


1. The order confirmation message appears in the target div.
2. The order summary gets refreshed.
3. The customer's balance is updated.
4. The recent orders list is refreshed.


All of these updates happen simultaneously, making it perfect for situations where you need to refresh multiple pieces of information after a successful operation.

## Conclusion


Fully appreciating the power of `mx-on-success` requires a touch of imagination.


Picture an exceptionally sophisticated admin panel for a powerful web application.


Now, imagine a demanding client requesting a feature that updates multiple sections of a page *entirely independently of one another*.


For instance, one part of the page could display a live stock market chart, another part of the page could display real-time enquiries, a third part of the page might track the price of Bitcoin, and yet another part of the page could display internal messages sent by logged-in users.


**Building such a dynamic application *without* Trongate MX would be an immense challenge! Even for a JavaScript guru, it would involve wrangling with observables, subscriptions, and multiple layers of complex, esoteric code.**


Fortunately, Trongate MX simplifies this process. Now, you can effortlessly declare and activate the components you need, making even the most demanding applications easy to build.


This is why the `mx-on-success` attribute is arguably one of the most important features in Trongate MX.

