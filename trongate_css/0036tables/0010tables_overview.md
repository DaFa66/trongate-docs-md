# Tables Overview


Trongate CSS provides clean, responsive table styling out of the box. Tables are automatically styled for readability with alternating row colors, borders, and hover effects - all without requiring additional classes.

## Basic Example


Here's a simple table that demonstrates the default styling:

| Name | Position | Location |
| ---|---|---|
| John Smith | Software Engineer | London |
| Sarah Johnson | UX Designer | Berlin |
| Michael Brown | Project Manager | New York |
```html
<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Position</th>
            <th>Location</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>John Smith</td>
            <td>Software Engineer</td>
            <td>London</td>
        </tr>
        <tr>
            <td>Sarah Johnson</td>
            <td>UX Designer</td>
            <td>Berlin</td>
        </tr>
        <tr>
            <td>Michael Brown</td>
            <td>Project Manager</td>
            <td>New York</td>
        </tr>
    </tbody>
</table>
```

## Table Structure


A well-structured HTML table should include both `<thead>` and `<tbody>` sections. While these tags are technically optional, using them provides several benefits:

### The <thead> Element


- Defines the header section of your table
- Contains one or more rows (`<tr>`) of header cells (`<th>`)
- Automatically styled with the primary theme color in Trongate CSS
- Helps screen readers identify header information for accessibility
- Makes it easier to style header cells differently from body cells

### The <tbody> Element


- Contains the main content of your table
- Groups table rows (`<tr>`) and data cells (`<td>`)
- Enables features like scrollable tables with fixed headers
- Helps maintain table structure when rows are dynamically added or removed
- Improves readability of your HTML code

## Default Features


Trongate CSS applies the following styles to tables automatically:


- Full-width layout that adapts to container size
- Consistent padding (0.7em) for all cells
- Borders around all cells using the primary theme color
- Alternating row colors for better readability
- Hover effect on table rows
- Themed header styling using the primary color
- White text color for header cells for optimal contrast

## Basic Table Example with Data


Here's a more comprehensive example showing a data-rich table with multiple columns:

| Product ID | Product Name | Category | Price | Stock |
| ---|---|---|---|---|
| 001 | Wireless Mouse | Electronics | $29.99 | 45 |
| 002 | USB-C Cable | Accessories | $12.99 | 132 |
| 003 | Bluetooth Speaker | Electronics | $79.99 | 28 |
| 004 | Laptop Stand | Accessories | $34.99 | 56 |
```html
<table>
    <thead>
        <tr>
            <th>Product ID</th>
            <th>Product Name</th>
            <th>Category</th>
            <th>Price</th>
            <th>Stock</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>001</td>
            <td>Wireless Mouse</td>
            <td>Electronics</td>
            <td>$29.99</td>
            <td>45</td>
        </tr>
        <!-- Additional rows... -->
    </tbody>
</table>
```

> [!NOTE]
> **Just To Let You Know...**
>
> While tables are great for displaying tabular data, they should not be used for layout purposes. For layout, use CSS Grid or Flexbox instead.


> [!TIP]
> **Best Practices**
>
> - Always use `<th>` elements for header cells instead of `<td>` with bold text.
> - Include both `<thead>` and `<tbody>` tags for better structure.
> - Keep tables as simple as possible - avoid nested tables.
> - Use appropriate column widths to prevent content from being squeezed.
> - Consider using a container class to control the table's maximum width.


