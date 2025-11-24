# Managing Browser URL State


Trongate MX introduces the ability to manage the browser's URL state directly from your HTML, eliminating the need for custom JavaScript. This feature is perfect for creating dynamic, URL-driven interfaces such as filtering, sorting, or navigating through content-rich web applications.

## Basic Usage


The `mx-push-url` attribute lets you update the browser's URL dynamically whenever an element is interacted with. When set to "true", it will push the request URL into the browser's history, making your application behave like a true single-page application (SPA). For example, you can use it with a dropdown menu to update the URL dynamically:


Here's how to create a category selector using pure HTML:

```html
<select id="category-selector" 
  mx-get="products/fetch_by_category/${this.value}" 
  mx-target="#product-list" 
  mx-push-url="true" 
  mx-trigger="change">
  <option value="electronics">Electronics</option>
  <option value="fashion">Fashion</option>
  <option value="home">Home</option>
</select>
```


The same category selector can be created using Trongate's form_dropdown() function:

```vf
<?php
$options = [
    'electronics' => 'Electronics',
    'fashion' => 'Fashion',
    'home' => 'Home'
];

$attributes = [
    'id' => 'category-selector',
    'mx-get' => 'products/fetch_by_category/${this.value}',
    'mx-target' => '#product-list',
    'mx-push-url' => 'true',
    'mx-trigger' => 'change'
];

echo form_dropdown('category', $options, '', $attributes);
?>
```


In this example, when the user selects "Fashion," the browser URL will update to match the request URL (`/products/fetch_by_category/fashion`), and a GET request fetches the corresponding products for display in the `#product-list` element.

> [!NOTE]
> **Just To Let You Know...**
>
> ### Technical Information
> 
> 
> When `mx-push-url="true"` is used, Trongate MX integrates with the browser's History API to create a seamless single-page navigation experience. After a successful AJAX request (status codes 200-299), the request URL is pushed to the browser's history stack. When users click the browser's back/forward buttons, Trongate MX intercepts these navigation events and automatically triggers the appropriate requests to restore the previous state - all without requiring page reloads. If the application state cannot be restored, the system falls back to a standard page reload to ensure consistent behavior.


### Pagination Example


The example below demonstrates using `mx-push-url` for pagination. When a user clicks on a page number, the URL updates dynamically to match the request URL.


Using pure HTML:

```vf
<button mx-get="posts/fetch_page/2" 
        mx-target="#posts-container" 
        mx-push-url="true">Page 2</button>
```


The same pagination button can be created using Trongate's form_button() function:

```vf
<?php
$attributes = [
    'mx-get' => 'posts/fetch_page/2',
    'mx-target' => '#posts-container',
    'mx-push-url' => 'true'
];

echo form_button('page_btn', 'Page 2', $attributes);
?>
```

## Pure HTML Form Example


The code sample below demonstrations the `mx-push-url` attribute being used with pure HTML elements including a form and two buttons.

```html
<!-- Filtering products -->
<button mx-get="products/filter/${this.value}" 
        mx-target="#product-grid" 
        mx-push-url="true">Filter Products</button>

<!-- Loading user profiles -->
<button mx-get="users/view/${this.value}" 
        mx-target="#user-profile" 
        mx-push-url="true">View Profile</button>

<!-- Search results -->
<form mx-get="search/results/${this.value}" 
      mx-target="#search-results" 
      mx-push-url="true">
  <input type="text" name="query">
  <button type="submit">Search</button>
</form>
```

> [!TIP]
> **Best Practices**
>
> - Use `mx-push-url="true"` when you want the browser URL to reflect the current state of your application.
> - Ensure your server-side routes match the URLs that will be pushed to the browser history.
> - Test browser back/forward navigation thoroughly to ensure a smooth user experience.
> - Remember that the URL is only updated after successful requests (status codes 200-299).
> - Consider using meaningful URL segments that reflect the current application state.


## Limitations


- The feature relies on browser support for the History API (modern browsers only).
- URLs are only updated after successful AJAX requests.
- The pushed URL will always match the request URL specified in the mx-get attribute.

## Summary


The `mx-push-url` feature in Trongate MX provides a simple way to manage browser history in single-page applications. By setting `mx-push-url="true"`, you ensure that your application's URLs stay synchronized with its state, enabling proper bookmarking and browser navigation without any custom JavaScript code.

