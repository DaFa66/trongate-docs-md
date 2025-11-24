# Table Variations


While Trongate CSS provides excellent default table styling, you may want to customize tables for specific use cases. This guide explores various ways to modify table appearance and behavior.

## Compact Tables


You can create more compact tables by adjusting cell padding using custom CSS:

| ID | Name | Status |
| ---|---|---|
| 1 | John Doe | Active |
| 2 | Jane Smith | Pending |
```html
<table class="compact-table">
    <thead>
        <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Status</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1</td>
            <td>John Doe</td>
            <td>Active</td>
        </tr>
        <!-- More rows... -->
    </tbody>
</table>

<style>
.compact-table th,
.compact-table td {
    padding: 0.3em;
}
</style>
```


---

## Custom Header Colors


You can modify table header colors using CSS variables or direct color values:

| Package | Price | Features |
| ---|---|---|
| Basic | $19.99 | Essential features |
| Pro | $49.99 | Advanced features |
```html
<table class="custom-header">
    <!-- Table content... -->
</table>

<style>
.custom-header th {
    background-color: var(--secondary);
    border-color: var(--secondary-dark);
}
</style>
```

> [!TIP]
> **Best Practices**
>
> Remember that while customizing tables, it's important to maintain good contrast ratios for accessibility. Test your custom styles with different color combinations to ensure readability.



---

## Highlighted Rows


You can highlight specific rows for emphasis using custom classes:

| Plan | Users | Price |
| ---|---|---|
| Basic | 5 users | $29/mo |
| Professional | 25 users | $99/mo |
| Enterprise | Unlimited | $299/mo |
```html
<tr class="highlight-row">
    <td>Professional</td>
    <td>25 users</td>
    <td>$99/mo</td>
</tr>

<style>
tr.highlight-row {
    background-color: yellow;
}
</style>
```


---

## Responsive Tables


For better mobile display, wrap your table in a container with horizontal scroll:

| Product | Category | Price | Stock | Rating | Actions |
| ---|---|---|---|---|---|
| Premium Laptop | Electronics | $1,299.99 | 45 | 4.5/5 | Edit \| Delete |
| Wireless Mouse | Accessories | $49.99 | 132 | 4.8/5 | Edit \| Delete |
```html
<div class="table-responsive">
    <table>
        <!-- Table content... -->
    </table>
</div>

<style>
.table-responsive {
    overflow-x: auto;
    margin: 1em 0;
}
</style>
```


---

## Custom Cell Alignment


You can align cell content using text alignment classes:

| Product | Quantity | Price |
| ---|---|---|
| Premium Widget | 5 | $99.99 |
| Basic Widget | 3 | $49.99 |
```html
<table>
    <thead>
        <tr>
            <th class="text-left">Product</th>
            <th class="text-center">Quantity</th>
            <th class="text-right">Price</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td class="text-left">Premium Widget</td>
            <td class="text-center">5</td>
            <td class="text-right">$99.99</td>
        </tr>
        <!-- More rows... -->
    </tbody>
</table>
```


---

## Status-Based Row Colors


Inside of defining a brand new color/class for table rows, you can also access pre-existing [CSS variables](documentation/display/trongate_css/css-fundamentals/css-variables) to create status-based row colors.  This technique guarantees that your table row styling is kept in alignment with underlying CSS variables.  For example:

| Order ID | Customer | Status |
| ---|---|---|
| 001 | John Doe | Completed |
| 002 | Jane Smith | Pending |
| 003 | Bob Wilson | Cancelled |
```html
<table>
    <thead>
        <tr>
            <th>Order ID</th>
            <th>Customer</th>
            <th>Status</th>
        </tr>
    </thead>
    <tbody>
        <tr class="status-row-success">
            <td>001</td>
            <td>John Doe</td>
            <td>Completed</td>
        </tr>
        <tr class="status-row-warning">
            <td>002</td>
            <td>Jane Smith</td>
            <td>Pending</td>
        </tr>
        <tr class="status-row-danger">
            <td>003</td>
            <td>Bob Wilson</td>
            <td>Cancelled</td>
        </tr>
    </tbody>
</table>

<style>
tr.status-row-success {
    background-color: color-mix(in srgb, var(--success) 10%, transparent);
}
tr.status-row-warning {
    background-color: color-mix(in srgb, var(--warning) 10%, transparent);
}
tr.status-row-danger {
    background-color: color-mix(in srgb, var(--danger) 10%, transparent);
}
</style>
```

> [!NOTE]
> **Just To Let You Know...**
>
> ### What is color-mix()?
> 
> 
> The `color-mix()` function in CSS lets you blend two colours together to create new ones. It's a simple way to create effects like transparent overlays, gradients, and custom colour combinations dynamically.
> 
> #### How Does It Work?
> 
> 
> The function combines two colours in a specified colour space. Here's the syntax:
> 
> ```css
> color-mix(in <color-space>, <color1> <percentage>, <color2>);
> ```
> 
> #### Example Use Case
> 
> 
> Here's how you can blend 10% of your primary colour with transparency:
> 
> ```css
> background-color: color-mix(in srgb, var(--primary) 10%, transparent);
> ```
> 
> #### Understanding sRBG
> 
> 
> The 'srgb' value in the color-mix() function refers to the sRGB (Standard RGB) colour space, which is a commonly used colour space for web and digital design.  **sRGB** defines how colours are represented and rendered on screens. It is the default colour space for most web content and displays.
> 
> #### Browser Support and Fallback
> 
> 
> Modern browsers support `color-mix()`. To ensure compatibility with older browsers, provide a fallback:
> 
> ```css
> background-color: var(--primary); /* Fallback */
> background-color: color-mix(in srgb, var(--primary) 10%, transparent);
> ```
> 
> #### Pro Tips
> 
> 
> - Adjust percentages to fine-tune blending effects.
> - Combine with CSS variables to maintain consistent theming.
> - Use it for hover effects, overlays, and accent colours in your designs.



---

## Advanced Customization Tips


- Use CSS variables for consistent color theming across tables
- Consider using `max-height` with `overflow-y: auto` for scrollable table bodies
- Add `white-space: nowrap` to prevent content wrapping in specific cells
- Use `width` or `min-width` on columns to control their sizing
- Consider using the container classes (e.g., `container-sm`) to control table width

