# Container Classes


Trongate CSS provides a range of container classes to help control content width and maintain consistent margins across different screen sizes, all while remaining highly responsive.

## Default Container


The default container class sets content width to 90% of the viewport with a maximum width of 940px, ensuring readability and proper content organization across all device sizes.

```css
.container {
  width: 90%;
  max-width: 940px;
  margin: 0 auto;
  padding: 1em;
}
```

## Container Sizes


Trongate CSS offers seven container variations to accommodate different content needs:

> [!NOTE]
> **Just To Let You Know...**
>
> The visual examples below are shown within the documentation's own container, so they cannot demonstrate their true maximum widths. To see the actual container widths in action, try the code examples on your own page.


container-xxs (450px)
container-xs (640px)
container-sm (760px)
container-md (820px)
container (940px)
container-lg (960px)
container-xl (1100px)
container-xxl (1300px)
```html
<div class="container-xxs">Extra extra small container content</div>
<div class="container-xs">Extra small container content</div>
<div class="container-sm">Small container content</div>
<div class="container-md">Medium container content</div>
<div class="container">Default container content</div>
<div class="container-lg">Large container content</div>
<div class="container-xl">Extra large container content</div>
<div class="container-xxl">Extra extra large container content</div>
```

> [!TIP]
> **Best Practices**
>
> All container classes maintain 90% width on smaller screens and automatically center themselves using margin: 0 auto. The 1em padding ensures content doesn't touch the container edges.


## Container Specifications


Each container class is optimized for specific use cases:


- **container-xxs (450px)**: Perfect for login forms, small widgets, and focused content areas
- **container-xs (640px)**: Ideal for simple forms, narrow content layouts, and focused reading experiences
- **container-sm (760px)**: Great for blog posts, articles, and medium-width content
- **container-md (820px)**: Balanced width for general content pages
- **container (940px)**: The default choice for most webpage content
- **container-lg (960px)**: Slightly wider than default for more spacious layouts
- **container-xl (1100px)**: Suitable for dashboards and data-rich interfaces
- **container-xxl (1300px)**: Best for full-width applications and complex layouts

> [!NOTE]
> **Just To Let You Know...**
>
> All container classes automatically adjust their width to 90% on mobile devices, ensuring a consistent margin on smaller screens while maintaining content readability.


## Common Use Cases


Here's an example of nested containers for creating complex layouts:

```html
<div class="container-xl">
  <div class="card">
    <div class="card-heading">Dashboard</div>
    <div class="card-body">
      <div class="container-sm">
        <!-- Centered content within a wide container -->
        <p>This content is centered within a wider container</p>
      </div>
    </div>
  </div>
</div>
```

## Summary


Trongate's container system provides:


- Eight predefined container widths for various use cases
- Consistent 90% width on mobile devices
- Automatic horizontal centering
- Built-in padding for content spacing
- Responsive behavior without additional configuration

