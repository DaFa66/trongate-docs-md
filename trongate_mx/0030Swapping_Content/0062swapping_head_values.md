# Dynamic Browser Tabs


With the `mx-swap-title` attribute, you can update your browser tab titles instantly as users navigate through your content - no page reloads required!

## Why Update Page Titles?


Imagine you're building a movie review website. When visitors browse different films, you'd want the browser tab to show which film they're currently viewing. This helps users:


- Quickly find your page among multiple browser tabs
- Create accurate bookmarks for specific content
- See meaningful titles in their browser history

## How to Update Page Titles


Using `mx-swap-title` is straightforward. Here's a simple example:

```vf
<?php
$btn_attr = [
    'mx-get' => 'films/view/123',
    'mx-target' => '#film-details',
    'mx-swap-title' => 'true'
];
echo form_button('view_film_btn', 'View Film Details', $btn_attr);
?>

<div id="film-details"></div>
```


For an HTML-only approach, here's the corresponding code:

```html
<button mx-get="films/view/123"
        mx-target="#film-details"
        mx-swap-title="true">View Film Details</button>

<div id="film-details"></div>
```

## Understanding the Code


Let's break down what's happening:


1. When the button is clicked, it fetches content from `films/view/123`.
2. The film details are loaded into the `#film-details` div.
3. The page title automatically updates to match the page title from the target API endpoint.

> [!NOTE]
> **Just To Let You Know...**
>
> **Important:** Your server response needs to include a `<title>` tag. For example:
> 
> ```html
> <title>The Matrix (1999) - Movie Reviews</title>
> ```


## Real-World Example


Here's how you might use this in a product catalog:

```vf
<?php
$btn_attr = [
    'mx-get' => 'shop/product/456',
    'mx-target' => '#product-display',
    'mx-swap-title' => 'true'
];

echo form_button('view_product', 'View Product', $btn_attr);
?>

<div id="product-display"></div>
```


Now when customers browse different products, your page title will automatically update to show the current product name - perfect for when they have multiple items open in different tabs!

## Top Tips for Title Swapping

> [!TIP]
> **Best Practices**
>
> - **Keep Titles Descriptive:** Include both the specific content (e.g., product name) and your site name
> - **Be Consistent:** Maintain a consistent title format across all your pages
> - **Test Navigation:** Ensure titles update correctly when users use browser back/forward buttons
> - **Mind Your Length:** Keep titles under 60 characters - they'll look better in browser tabs and history


## Summary


Dynamic page titles might seem like a small detail, but they significantly improve the user experience of your web applications. With `mx-swap-title`, Trongate MX makes it easy to implement this professional touch. Just add the attribute to your elements, ensure your server returns the right title tags, and you're ready to go!

