# Element Removal


Trongate MX makes it super easy to remove elements from your webpage with its `mx-remove` attribute. You won't need to write a single line of JavaScript - it just works!

## Demonstration


Try clicking on the 'Remove' buttons and notice how the items are immediately removed from the page.

- BreadRemove **
- MilkRemove **
- EggsRemove **
> [!NOTE]
> **Just To Let You Know...**
>
> The `mx-remove` attribute only removes elements from the current page - it doesn't delete anything from your database or make any HTTP requests.


## How Does It Work?


The `mx-remove` attribute can work in two specific ways:

### 1. Remove Immediate Parent Element


When you set `mx-remove="true"`, it will remove the clicked element's immediate parent.

```html
<div class="notification">
  <span>
    <button mx-remove="true">×</button>
  </span>
  Your message has been sent!
</div>
```


In this example, clicking the button removes the surrounding **span element**, since it's the button's immediate parent.

### 2. Remove Specific Ancestor Using Selectors


When you provide a CSS selector value to mx-remove, it will remove the closest ancestor that matches that selector.

```html
<div class="notification">
  <span>
    <button mx-remove=".notification">×</button>
  </span>
  Your message has been sent!
</div>
```


Here, clicking the button removes the entire **notification div** since it matches the .notification selector.

## Basic Examples

### Simple List Item Removal

```html
<ul>
    <li>Rolex Explorer 2 
        <button mx-remove="true">×</button>
    </li>
    <li>Omega Seamaster 
        <button mx-remove="true">×</button>
    </li>
    <li>Tag Heuer Carrera 
        <button mx-remove="true">×</button>
    </li>
</ul>
```


The buttons above remove the closest li ancestor when clicked, deleting entire list items.

### Alert Dismissal

```html
<div class="alert alert-success">
  <p>Changes saved successfully!</p>
  <button mx-remove=".alert">×</button>
</div>
```


Clicking the × button removes the entire alert because it targets the closest element with the 'alert' class.

## What's The Point?


You might wonder: *"If mx-remove doesn't make HTTP requests or affect my database, why would I use it?"*


Good question! The beauty of `mx-remove` lies in its simplicity and flexibility. While it only modifies the page display on its own, it becomes incredibly powerful when combined with other MX attributes like `mx-post`. This allows you to remove elements visually while handling server-side operations behind the scenes.

## Practical Use Case: Shopping Cart with Error Handling


Here's how you can create a robust shopping cart system where items are removed visually and server communication is handled seamlessly.

### Example Code: Cart Item Removal

```vf
<div class="cart-item"><br>
    <img src="product.jpg"><br>
    <div class="details"><br>
      <h3>Blue T-Shirt</h3><br>
      <p>$19.99</p><br>
    </div><br><br>
    <?php<br>
    $attr = [<br>
      'mx-post' => 'cart/remove/'.$item_id,<br>
      'mx-remove' => '.cart-item',<br>
      'mx-target' => '#cart-total',<br>
      'mx-redirect-on-error' => 'true'<br>
    ];<br>
    echo form_button('remove_btn', 'Remove', $attr);<br>
    ?><br>
</div>
```


Below is the *same solution*, expressed **without** using Trongate's form_button() function:

```vf
<div class="cart-item">
    <img src="product.jpg">
    <div class="details">
      <h3>Blue T-Shirt</h3>
      <p>$19.99</p>
    </div>
    <button mx-post="cart/remove/<?= $item_id ?>"
            mx-remove=".cart-item"
            mx-target="#cart-total"
            mx-redirect-on-error="true">Remove</button>
</div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> Even though no data is being explicitly posted in the deletion request, there's a very important reason we're using `mx-post` here. According to REST principles, DELETE operations should be made using either POST or DELETE HTTP methods, not GET.
> 
> 
> This is because:
> 
> 
> - GET requests should be idempotent (they shouldn't change server state).
> - GET requests are often cached by browsers and can be pre-fetched.
> - GET requests can be accidentally triggered (e.g., by search engine crawlers).
> 
> 
> While `mx-delete` would also be valid here (and arguably more semantically correct), `mx-post` is often chosen because:
> 
> 
> - Some legacy systems might not properly handle DELETE requests.
> - Some firewalls might block DELETE methods.
> - Older browsers might not fully support DELETE methods.
> 
> 
> So while we could use either `mx-post` or `mx-delete`, using `mx-post` for deletion operations is a common and safe choice. The key point is that we're avoiding `mx-get` for operations that modify server data.


### How It Works


- **Immediate Feedback:** When the "Remove" button is clicked, the cart item disappears from the page instantly thanks to `mx-remove`.
- **Server Communication:** The `mx-post` attribute sends a request to the server to update the database.
- **Error Handling:** If the server responds with an error (e.g., an expired session), the `mx-redirect-on-error` attribute redirects the user to a specified error page.

> [!NOTE]
> **Just To Let You Know...**
>
> While using `mx-remove` with `mx-post` can provide immediate visual feedback, a more conventional approach is to refresh the affected content **after** server confirmation. Here's an example:
> 
> ```vf
> <?php
> $btn_attr = [
>     'mx-post' => 'members/delete_record/'.$row->id,
>     'mx-indicator' => '#spinner-'.$row->id,
>     'mx-on-success' => '.response'  // Refreshes the container on success
> ];
> echo form_button('delete_btn', 'Delete', $btn_attr);
> ?>
> ```
> 
> 
> This pattern ensures UI updates only occur after successful server operations, maintaining data consistency and providing clear visual feedback through spinners. It's particularly suitable for data-critical operations like deletions in admin interfaces.


### Backend Example: Handling Item Removal


Here's an example of the kind of code that could potentially be used for the item removal API endpoint.  This is just one of *many* possible methodologies.

```php
public function remove() {<br>

  // Fetch item ID from URL (making sure it's an integer)
  $item_id = segment(3, 'int');

  // Attempt remove item from shopping cart
  $result = $this->attempt_remove_from_cart($item_id);

  if ($result !== true) {
    http_response_code(400);
    echo 'cart/error'; // Redirects to an error page
    die();
  }

  http_response_code(200);
  echo $this->cart->get_total(); // Returns updated cart total on success
}
```

> [!TIP]
> **Best Practices**
>
> - Use `mx-remove="true"` to remove the immediate parent element.
> - Use `mx-remove="<CSS Selector>"` to target and remove a specific ancestor.
> - Combine `mx-remove` with attributes like `mx-post` or `mx-target` to handle backend operations while updating the UI.
> - 
>     Remember:
> 
> 1. Class selectors require a dot (e.g., `.notification`).
> 2. ID selectors require a hash symbol (e.g., `#message`).
> 
> 
> - Test error scenarios to ensure robust error handling.


## Technical Details


When a click event occurs on an element with the `mx-remove` attribute, Trongate MX performs the following steps:


1. **Check Attribute Value**
The system checks the attribute value and processes it in one of two ways:


- For `mx-remove="true"`: Identifies the immediate parent using `parentElement`
- For `mx-remove="selector"`: Finds the closest matching ancestor using `closest(selector)`


2. **Update DOM**
The matched element is immediately removed from the DOM, with all changes applied instantly without additional JavaScript.



> [!NOTE]
> **Just To Let You Know...**
>
> - **Client-Side Only:**`mx-remove` doesn't send HTTP requests or modify your database. Combine it with `mx-post` for server-side operations.
> - **Immediate Changes:** Removal is instant and cannot be undone without refreshing the page.
> - **Value Requirements:** The `mx-remove` attribute must be set to either `true` or a valid CSS selector.
> - **Versatility:** Works with any clickable element (e.g., buttons, links).


## Summary


The `mx-remove` attribute lets your remove UI elements easily. Whether you're removing a notification, dismissing an alert, or updating a shopping cart, `mx-remove` provides a simple yet powerful solution. When paired with other MX attributes, it becomes a complete tool for managing client-side interactions with minimal effort.

