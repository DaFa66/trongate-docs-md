# Pagination


Trongate CSS provides a sleek, user-friendly pagination system that ensures smooth navigation across multiple pages. By following the correct HTML structure, you can effortlessly implement consistent and visually appealing pagination components.

## Basic Pagination


To create a basic pagination component, wrap your pagination links inside a container with the `.pagination` class:

[«](#)[1](#)[2](#)[3](#)[4](#)[»](#)
```html
<div class="pagination">
  <a href="#">&laquo;</a>
  <a href="#">1</a>
  <a href="#" class="active">2</a>
  <a href="#">3</a>
  <a href="#">4</a>
  <a href="#">&raquo;</a>
</div>
```

## Styling Highlights


- Rounded corners for the first and last links.
- Hover effects for interactive feedback.
- Active links are styled with the primary colour for emphasis.
- Consistent spacing and clean borders.

## Using Multiple Pagination Blocks


Place pagination components at the top and bottom of your content. The first pagination block includes a bottom margin for spacing, while subsequent blocks add a top margin for consistency:

[«](#)[1](#)[2](#)[3](#)[»](#)
Content Area
[«](#)[1](#)[2](#)[3](#)[»](#)
```html
<!-- Top pagination -->
<div class="pagination">
  <a href="#">&laquo;</a>
  <a href="#" class="active">1</a>
  <a href="#">2</a>
  <a href="#">3</a>
  <a href="#">&raquo;</a>
</div>

<!-- Content area -->
<div class="content">
  <!-- Your content here -->
</div>

<!-- Bottom pagination -->
<div class="pagination">
  <a href="#">&laquo;</a>
  <a href="#" class="active">1</a>
  <a href="#">2</a>
  <a href="#">3</a>
  <a href="#">&raquo;</a>
</div>
```

## Extended Example


For pages with more content, you can extend the pagination component to include additional page numbers and states:

[«](#)[1](#)[2](#)[3](#)[4](#)[5](#)[6](#)[7](#)[»](#)
```html
<div class="pagination">
  <a href="#">&laquo;</a>
  <a href="#">1</a>
  <a href="#">2</a>
  <a href="#" class="active">3</a>
  <a href="#">4</a>
  <a href="#">5</a>
  <a href="#">6</a>
  <a href="#">7</a>
  <a href="#">&raquo;</a>
</div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> By default, the previous and next links use `«` and `»`. You can replace these with icons or other symbols for custom designs.


