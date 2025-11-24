# Regarding View File Syntax


In Trongate MX, there are two main ways to create form elements and other HTML content. This section will guide you through both approaches:


1. Using Trongate's Form Helper Functions
2. Writing Plain HTML


Let's explore both approaches.


---

## 1) Using Trongate's Form Helper Functions


Trongate's form helper functions provide a clean and consistent way to generate HTML elements. These functions are designed to streamline your code and ensure it follows best practices.


For example, here's how to create a form button using Trongate's form_button() form helper:

```vf
<?php
echo form_button('my_btn', 'Click Me');
?>
```


This generates the following HTML:

```html
<button type="button" name="my_btn" value="Click Me">Click Me</button>
```


Now, let's look at how to add attributes to create more complex elements.  This can be achieved by passing in an array of key-value pairs.  For example, a button that triggers an API call (with Trongate MX) could be rendered using the following syntax:

```vf
<?php
$attributes = [
   'mx-get' => 'store/fetch_items',
   'mx-target' => '#items-target'
];
echo form_button('fetch_items_btn', 'Load Items', $attributes);
?>
```


This generates the following HTML:

```html
<button type="button" name="fetch_items_btn" value="Load Items" mx-get="store/fetch_items" mx-target="#items-target">Load Items</button>
```

> [!NOTE]
> **Just To Let You Know...**
>
> When using form helpers like form_button(), certain attributes, such as the 'name' attribute, are rendered by default. However, not *all* of these attributes are essential for Trongate MX to function properly.



---

## 2) Writing Pure HTML


While Trongate's form helpers are recommended, you can *still* write pure HTML for form elements, if you prefer. Here's an alternative syntax the produces the same result as the example shown above:

```html
<button mx-get="store/fetch_items" 
        mx-target="#items-target">Load Items</button>
```


**Both approaches are fully supported and will function correctly with Trongate MX.**


---

## The Pros And Cons Of These Approaches


The choice between using form helpers or writing plain HTML is entirely up to you. Both methods will work seamlessly with Trongate MX.

Form Helpers
### Pros


- Consistent code structure across your application.
- Built-in security features and sanitization.
- Shorter, more readable code in complex scenarios.

### Cons


- Requires learning the helper function syntax.
- Slightly more typing required for very simple elements.
- May generate additional attributes you don't need.
Plain HTML
### Pros


- Complete control over the output HTML.
- No learning curve for developers familiar with HTML.
- Familiar syntax for developers experienced with libraries like HTMX.

### Cons


- No built-in security features.
- May require excessive code for complex forms.

Regardless of the method you choose, Trongate MX's attributes (such as `mx-get`, `mx-target`, etc.) will function the same way in both scenarios. The underlying functionality remains consistent.

