# Dynamic URL Construction


Trongate MX now supports dynamic URL construction for all HTTP method attributes, allowing you to create more flexible and responsive user interfaces. This feature enables you to include dynamic values in your request URLs, making your web applications more interactive and data-driven.

## Basic Usage


The HTTP method attributes (`mx-get`, `mx-post`, `mx-put`, `mx-patch`, and `mx-delete`) now support placeholders in the URL that will be replaced with the current value of the element. The syntax uses `${this.value}` to indicate where the element's value should be inserted.


In the following example, if the user selects "User 2", the GET request will be sent to "api/users/2".

```html
<select id="user-selector" 
    mx-get="api/users/${this.value}" 
    mx-target="#user-details"
    mx-trigger="change">
    <option value="1">User 1</option>
    <option value="2">User 2</option>
    <option value="3">User 3</option>
</select>
```


The code below demonstrates the same solution, but written using Trongate's form_dropdown() function.

```vf
<?php
$options = [
  '1' => 'User 1',
  '2' => 'User 2',
  '3' => 'User 3'
];

$attributes = [
  'id' => 'user-selector',
  'mx-get' => 'api/users/${this.value}',
  'mx-target' => '#user-details',
  'mx-trigger' => 'change'
];

echo form_dropdown('users', $options, '', $attributes);
?>
```

## How It Works


When an HTTP request is triggered, Trongate MX will:


1. Detect the `${this.value}` placeholder in the URL
2. Replace it with the current value of the element
3. Send the HTTP request to the resulting URL

## Supported HTTP Methods


This feature works with all HTTP method attributes in Trongate MX:


- `mx-get`
- `mx-post`
- `mx-put`
- `mx-patch`
- `mx-delete`

## More Examples


The code sample below demonstrates how to create a dropdown menu that fetches product details dynamically. When a user selects a different product from the dropdown, it triggers a GET request to fetch that specific product's information, which is then displayed in an element with the ID 'product-details'.

### Fetching Product Details

```vf
&lt;?php
$options = [
    '1' => 'Product 1',
    '2' => 'Product 2'
];

$attributes = [
    'mx-get' => 'api/products/${this.value}',
    'mx-target' => '#product-details',
    'mx-trigger' => 'change'
];

echo form_dropdown('products', $options, '', $attributes);
?&gt;

<div id="product-details"></div>
```

### Checkbox Example


The code sample below demonstrates how to toggle the visibility of archived items. When the checkbox is clicked, it sends a GET request using the checkbox's value (1 when checked, 0 when unchecked) to fetch the appropriate content.

```vf
<?php
$attributes = [
    'mx-get' => 'api/products/archived/${this.value}',
    'mx-target' => '#products-list',
    'mx-trigger' => 'change',
    'value' => '0'
];

echo form_checkbox('show_archived', '1', false, $attributes);
echo form_label('Show Archived Products');
?>

<div id="products-list"></div>
```

### Hotel Booking Example


The code sample below demonstrates a hotel booking scenario. When the user changes the number of nights, it triggers a GET request to fetch the total price, which then updates in the price-display element.

```vf
<?php
$attributes = [
    'mx-get' => 'api/booking/calculate/${this.value}',
    'mx-target' => '#price-display',
    'mx-trigger' => 'change',
    'min' => '1',
    'max' => '30'
];

echo form_number('num_nights', '1', $attributes);
?>
<div id="price-display">
    <h3>Total Price: $150</h3>
    <p>(Based on 1 night stay)</p>
</div>
```

## Best Practices


- Use input elements that naturally provide meaningful values (dropdowns, checkboxes, number inputs, etc.)
- Ensure that the values used in your dynamic URLs are URL-safe
- Use appropriate `mx-trigger` attributes to respond to user interactions
- Remember that spaces and special characters in the value will be URL-encoded automatically
- For security reasons, validate and sanitize any dynamic values on the server-side before processing the request

> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** While this feature allows for dynamic URL construction, it's important to ensure that your server-side routing can handle these dynamic segments appropriately.


## Limitations


- This feature only supports `${this.value}` as a placeholder. More complex expressions are not evaluated.
- The placeholder can only represent the value property of the element that has the HTTP method attribute.
- Be cautious when using this feature with sensitive data, as the values become part of the URL.

## Summary


The dynamic URL construction feature enhances Trongate MX's capabilities by enabling interactive, data-driven interfaces without custom JavaScript. It's particularly useful for creating dynamic filters, toggles, and real-time calculations. The feature works best with form elements that naturally provide values, such as select dropdowns, checkboxes, and number inputs.

