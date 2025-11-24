# Flexbox Layout Classes


Trongate CSS provides utility classes for flexbox layouts, making it easy to create responsive and dynamic layouts. These classes control flex container direction, alignment, spacing, and item behavior.


---

## Basic Flex Containers


Use `.flex-row` or `.flex-column` to create flex containers with different directions:

Item 1
Item 2
Item 3
Item 1
Item 2
Item 3
```html
<!-- Row direction -->
<div class="flex-row">
    <div>Item 1</div>
    <div>Item 2</div>
    <div>Item 3</div>
</div>

<!-- Column direction -->
<div class="flex-column">
    <div>Item 1</div>
    <div>Item 2</div>
    <div>Item 3</div>
</div>
```


---

## Justify Content Classes


Control horizontal alignment using justify content classes:

OneTwo
OneTwo
OneTwo
OneTwo
OneTwo
```html
<div class="flex-row justify-start">
    <button>One</button>
    <button>Two</button>
</div>

<div class="flex-row justify-center">
    <button>One</button>
    <button>Two</button>
</div>

<div class="flex-row justify-end">
    <button>One</button>
    <button>Two</button>
</div>

<div class="flex-row justify-between">
    <button>One</button>
    <button>Two</button>
</div>

<div class="flex-row justify-around">
    <button>One</button>
    <button>Two</button>
</div>
```


---

## Align Items Classes


Control vertical alignment using align items classes:

Top
Center
Bottom
```html
<div class="flex-row align-start">
    <div>Top</div>
</div>

<div class="flex-row align-center">
    <div>Center</div>
</div>

<div class="flex-row align-end">
    <div>Bottom</div>
</div>
```


---

## Flex Grow


Use `.flex-grow` to allow an item to fill available space:

Fixed Width
> [!NOTE]
> **Just To Let You Know...**
>
> Trongate CSS file gives buttons a top margin. The relevant rule is:
> 
> ```css
> button,
> .button {
>   margin: 1em 0.1em 0 0;
> }
> ```
> 
> 
> To mitigate this, a class of `.mt-0` is added to the button, in the example.


```html
<div class="flex-row">
    <button class="mt-0">Fixed Width</button>
    <input type="text" class="flex-grow ml-1" placeholder="This input will grow">
</div>
```


---

## Flex Wrap


Flex containers in Trongate CSS allow you to control whether flex items stay on one line or wrap onto additional lines. This behaviour is controlled using the `.flex-wrap` and `.flex-nowrap` classes.


The `.flex-wrap` class makes items wrap onto the next line when they exceed the container's width, ensuring a responsive layout. In contrast, the `.flex-nowrap` class forces all items to remain on a single line, even if they overflow the container.

### Example: Wrapping Items


In this example, the `.flex-wrap` class is applied to a flex container. Items automatically wrap to a new line when there is not enough horizontal space in the container. Each button is styled with `flex: 1 1 auto;`, which allows them to grow and shrink proportionally, while also having consistent spacing through margins.

Button OneButton TwoButton ThreeButton FourButton Five
```html
<div class="flex-row flex-wrap" style="max-width: 400px; background: #f5f5f5; padding: 1em;">
    <button style="flex: 1 1 auto; margin: 0.5em; padding: 0.8em;">Button One</button>
    <button style="flex: 1 1 auto; margin: 0.5em; padding: 0.8em;">Button Two</button>
    <button style="flex: 1 1 auto; margin: 0.5em; padding: 0.8em;">Button Three</button>
    <button style="flex: 1 1 auto; margin: 0.5em; padding: 0.8em;">Button Four</button>
    <button style="flex: 1 1 auto; margin: 0.5em; padding: 0.8em;">Button Five</button>
</div>
```

### Example: Preventing Wrapping


The following example uses the `.flex-nowrap` class to keep all items on a single line. Notice how the container may overflow horizontally, which can be addressed with `overflow-x: auto;`. This is particularly useful for layouts where items need to remain in a single row.

Button OneButton TwoButton ThreeButton FourButton Five
```html
<div class="flex-row flex-nowrap" style="background: #f5f5f5; padding: 1em; overflow-x: auto;">
    <button style="flex: 0 0 auto; margin: 0.5em; padding: 0.8em;">Button One</button>
    <button style="flex: 0 0 auto; margin: 0.5em; padding: 0.8em;">Button Two</button>
    <button style="flex: 0 0 auto; margin: 0.5em; padding: 0.8em;">Button Three</button>
    <button style="flex: 0 0 auto; margin: 0.5em; padding: 0.8em;">Button Four</button>
    <button style="flex: 0 0 auto; margin: 0.5em; padding: 0.8em;">Button Five</button>
</div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> When working with flex wrap utilities, remember to combine them with appropriate margins, padding, and overflow styles to achieve the desired layout and usability. Wrapping is ideal for responsive designs, while preventing wrapping suits controlled, fixed-width layouts.



---

## Practical Example


Here's a common layout pattern combining multiple flex utilities:

Product Details
Price: $99.99


In stock: 42 units
View Item
```html
<div class="card">
    <div class="card-heading"> Product Details</div>
    <div class="card-body">
        <div class="flex-row justify-between">
            <div>
                <p class="mb-0">Price: $99.99</p>
                <p class="sm">In stock: 42 units</p>
            </div>
            <div class="flex-row align-center">
                <button>View Item</button>
            </div>
        </div>
    </div>
</div>
```

## Conclusion


Flexbox utilities in Trongate CSS empower developers to build responsive and highly customisable layouts with ease. By combining these utilities with margin, padding, and size classes, you can achieve precise alignment and spacing. Always keep in mind that flexbox properties only affect immediate child elements, making it essential to structure your HTML hierarchy thoughtfully for optimal results. Whether creating adaptive, wrapping designs or enforcing strict alignment, flexbox is a versatile tool to meet your layout needs.

