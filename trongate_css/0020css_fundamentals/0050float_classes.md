# Float Classes


Trongate CSS provides two utility classes for floating elements either to the left or right side of their container.


1. `.float-left`
2. `.float-right`


Within Trongate CSS, float classes are combined with relative positioning to maintain proper layout control. For example:

```css
.float-right {
  float: right;
  position: relative;
}
```


The combination of float and relative positioning ensures that floated elements maintain their position in the document flow while allowing other content to wrap around them.


---

## Left Float


To float an element to the left, use the `.float-left` class. This is commonly used for images that should have text wrapping around their right side.

```html
<div>
  <div class="float-left mr-1" style="width: 100px; height: 100px; background: #4682b4;"></div>
  <p>This text demonstrates how content wraps around a left-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a left-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a left-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a left-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a left-floated element. Notice how the text flows naturally around the blue box.</p>
</div>
```


Here's how it affects the layout:

This text demonstrates how content wraps around a left-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a left-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a left-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a left-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a left-floated element. Notice how the text flows naturally around the blue box.

---

## Right Float


To float an element to the right, use the `.float-right` class. This is useful for elements that should align to the right with content wrapping around their left side.

```html
<div>
  <div class="float-right ml-1" style="width: 100px; height: 100px; background: #4682b4;" ></div>
  <p>This text demonstrates how content wraps around a right-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a right-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a right-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a right-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a right-floated element. Notice how the text flows naturally around the blue box.</p>
</div>
```


Here's how it affects the layout:

This text demonstrates how content wraps around a right-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a right-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a right-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a right-floated element. Notice how the text flows naturally around the blue box.  This text demonstrates how content wraps around a right-floated element. Notice how the text flows naturally around the blue box.
> [!TIP]
> **Best Practices**
>
> Float classes are especially useful for working with images and other media elements within text content, enabling more dynamic and engaging layouts.
> 
> 
> When you float an item, such as an image, it's a good practice to add margins to create a gap between the floated element and the surrounding text. If you examine the two examples above closely, you'll notice this is achieved through the use of the `.ml-1` and `.mr-1` classes. These classes set a left margin of '1em' and a right margin of '1em', respectively.


## Summary


Trongate CSS provides two float utility classes:


- 
    `.float-left` – Floats elements to the left with relative positioning
  
- 
    `.float-right` – Floats elements to the right with relative positioning
  


Both classes include relative positioning to maintain proper layout control while allowing content to flow naturally around the floated elements.

