# Horizontal Rules


Horizontal rules (`<hr>`) in Trongate CSS provide clean dividing lines to separate content sections. They're styled minimally by default but can be easily customized.

## Default Styling


The basic horizontal rule is styled as a subtle gray line with consistent spacing:

```css
hr {
    border: 0;
    height: 1px;
    background: var(--border);
    margin: 2em 0;
}
```

> [!NOTE]
> **Just To Let You Know...**
>
> Note that the `border: 0` is used in combination with `height` and `background` to ensure consistent rendering across browsers.


## Basic Usage


The code below demonstrates how to add a horizontal rule to your page:

```html
<p class="text-center">Some content above the line</p>
<hr>
<p class="text-center">Some content below the line</p>
```


Here's how it looks:

This is some content above the horizontal rule.


---


This is some content below the horizontal rule.
## Customization Examples


Here are some common ways to customize horizontal rules:

### Colored Rule Example

```html
<hr style="background: var(--secondary);">
```


Here's the result (look closely and you'll notice it's using the `--secondary` color).

---
### Thicker Rule Example

```html
<hr style="height: 3px;">
```

---
### Shorter Rule with Center Alignment

```html
<hr style="width: 50%; margin: 2em auto;">
```

---
### Dotted Rule

```html
<hr style="background: none; border: none; border-top: 2px dotted var(--border); height: 0;">
```

---
## Spacing Considerations


By default, horizontal rules include:


- 2em margin above and below
- 1px height for the line itself
- Full width of the container

> [!TIP]
> **Best Practices**
>
> You can adjust the margins using Trongate's margin utility classes like `mt-1` or `mb-2` if needed.



Here's an example of some code that use margin utilities:

Default spacing:


---


Reduced top margin (mt-1):


---


Increased bottom margin (mb-3):


---
```html
<p class="text-center">Default spacing:</p>
<hr>
<p class="text-center">Reduced top margin (mt-1):</p>
<hr class="mt-1">
<p class="text-center">Increased bottom margin (mb-3):</p>
<hr class="mb-3">
```

## Summary


Trongate CSS horizontal rules provide:


- Clean, minimal default styling
- Consistent cross-browser rendering
- Easy customization options
- Proper vertical spacing


Use horizontal rules to create visual breaks between content sections while maintaining your site's design aesthetics.

