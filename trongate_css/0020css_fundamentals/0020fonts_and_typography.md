# Fonts And Typography


Trongate CSS uses Tahoma as its default font family, providing excellent readability across all modern browsers without requiring external font downloads.

## Default Font Settings

```css
body {
  font-family: Tahoma, Geneva, sans-serif;
  font-size: 1rem;
  color: #555;
  line-height: 1.5em;
}
```

> [!NOTE]
> **Just To Let You Know...**
>
> Tahoma was chosen because it's a web-safe font that's available on all modern devices, ensuring consistent rendering without loading external resources. It also has excellent readability characteristics and isn't as commonly used as Arial or Verdana, giving your site a distinctive look.


## Heading Sizes


Headings are pre-configured with appropriate sizes:

# Default 'h1' element

## Default 'h2' element

### Default 'h3' element

#### Default 'h4' element
```html
<h1 class="h1-default">Default 'h1' element</h1>
<h2 class="h2-default">Default 'h2' element</h2>
<h3 class="h3-default">Default 'h3' element</h3>
<h4 class="h4-default">Default 'h4' element</h4>
```

> [!TIP]
> **Best Practices**
>
> All font sizes use relative units (em, rem) rather than fixed pixels, ensuring proper scaling across different screen sizes and user preferences.


## Paragraph Text


Paragraphs are styled for optimal readability with comfortable line spacing:

Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quibusdam fuga saepe mollitia officiis labore repudiandae ea rem, eos tenetur dolores sequi ad blanditiis natus, minima commodi vitae odio modi quam.


Lorem ipsum dolor sit amet consectetur, adipisicing, elit. Sunt magni nihil autem doloremque est, facere dolorem culpa voluptatem amet aperiam adipisci consequuntur porro hic libero voluptates odit vel eum perferendis.
```html
<p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quibusdam fuga saepe mollitia officiis labore repudiandae ea rem, eos tenetur dolores sequi ad blanditiis natus, minima commodi vitae odio modi quam.</p>
<p>Lorem ipsum dolor sit amet consectetur, adipisicing, elit. Sunt magni nihil autem doloremque est, facere dolorem culpa voluptatem amet aperiam adipisci consequuntur porro hic libero voluptates odit vel eum perferendis.</p>
```


- Font color: #555 (easy on the eyes)
- Line height: 1.5em (good spacing between lines)
- Margin bottom: Creates natural spacing between paragraphs

## List Styling


Unordered lists are styled with clear spacing and custom bullets:

- Item 1
- Item 2
- Item 3
```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```


Ordered lists are styled in a similar manner with readability as a priority:

1. Apples
2. Oranges
3. Bananas
```html
<ol>
  <li>Apples</li>
  <li>Oranges</li>
  <li>Bananas</li>
</ol>
```

> [!NOTE]
> **Just To Let You Know...**
>
> Lists use circle bullets by default and have generous vertical margins to separate them from surrounding content. List items have slightly increased line height for better readability.


### Key Features


- Lists have 2em margins top and bottom
- Circle bullets for a clean look
- 1.8em line height for comfortable reading

> [!TIP]
> **Best Practices**
>
> The increased line height on list items (1.8em vs 1.5em for regular text) helps distinguish list content from regular paragraphs.


## Summary


That's all there is to it! No complicated font configurations or external dependencies - just clean, readable text that works everywhere. The typography system provides:


- Web-safe fonts that load instantly
- Consistent heading hierarchy
- Comfortable reading experience
- Well-spaced lists with distinct styling
- Relative units for better scaling

