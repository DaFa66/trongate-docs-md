# Text Alignment


In HTML, paragraphs and text blocks are usally aligned to the left by default. However, Trongate CSS offers three utility classes for controlling text alignment.  There are:


1. `.text-left`
2. `.text-right`
3. `.text-center`


Within the internals of Trongate CSS, each of the above text align classes are written with a declaration of `!important`.   For example:

```css
.text-left {
  text-align: left !important;
}
```


The `!important` declaration in CSS is used to give a style rule higher priority, overriding other conflicting rules for the same property on an element.

> [!WARNING]
> **Warning!**
>
> Normally, when working with CSS, using `!important` should generally be avoided as it can make debugging and maintaining CSS more difficult.



---

## Left Alignment


To align text to the left, use the `.text-left` class. This is the default alignment for text, but you can apply it explicitly if needed.

```html
<p class="text-left">This text is left-aligned.</p>
```


Here's the result:

This text is left-aligned.

---

## Right Alignment


To align text to the right, use the `.text-right` class. This can be useful for aligning elements like captions, footnotes, or certain types of content.

```html
<p class="text-right">This text is right-aligned.</p>
```


Here's the result:

This text is right-aligned.

---

## Center Alignment


To center text, use the `.text-center` class. This is commonly used for headings, titles, or any content you want to highlight in the center of the page.

```html
<p class="text-center">This text is centered.</p>
```


Here's the result:

This text is centered.
> [!TIP]
> **Best Practices**
>
> The `.text-center` class aligns the text to the center of the container, making it perfect for headlines or emphasizing certain content.


## Summary


Trongate CSS provides three text alignment classes for your convenience:


- 
    `.text-left` – Aligns text to the left.
  
- 
    `.text-right` – Aligns text to the right.
  
- 
    `.text-center` – Centers the text horizontally.
  


All classes use the `!important` declaration to ensure they take precedence over other styles, providing a quick and reliable way to manage text alignment across your website.

