# Responsive Design


Trongate CSS is built with responsive design principles at its core, ensuring websites adapt seamlessly across different device sizes. The framework implements a pragmatic mobile-first approach with a single breakpoint system.

## Mobile-First Features


Below is a summary of the key responsive features that are built into Trongate CSS by default:

### Responsive Images


Images automatically scale within their containers:

```css
img {
    max-width: 100%;
    height: auto;
}
```

> [!NOTE]
> **Just To Let You Know...**
>
> The combination of `max-width: 100%` and `height: auto` ensures images scale proportionally without exceeding their container width.


## Breakpoint System


Trongate CSS uses a single breakpoint at 550px for mobile adaptations. This streamlined approach simplifies responsive design while covering the most critical layout adjustments.

```css
@media screen and (max-width: 550px) {
    /* Mobile-specific adaptations */
}
```

## Mobile Adaptations


At the 550px breakpoint, several UI elements automatically adapt:

### Button Stacking


Buttons automatically stack vertically and expand to full width on mobile devices:

Primary ActionSecondary Action
```html
&lt;div&gt;
    &lt;button&gt;Primary Action&lt;/button&gt;
    &lt;button class="alt"&gt;Secondary Action&lt;/button&gt;
&lt;/div&gt;
```


On mobile screens (below 550px), these buttons will:


- Stack vertically
- Expand to 100% width
- Maintain proper spacing

### Modal Adaptations


Modals receive several mobile-optimized adjustments:

Click Me!
Example Modal
**
This is an example modal. It has a default margin top value of '12vh', which is defined as a CSS variable within Trongate CSS.


To learn more about working with modals  [click here](../0040cards_and_modals/0020working_with_modals.md).
Learn More **
```css
@media screen and (max-width: 550px) {
    .modal {
        max-height: 85vh;
        overflow-y: auto;
    }
    
    .modal-footer {
        flex-direction: column-reverse;
    }
}
```

> [!TIP]
> **Best Practices**
>
> To learn more about how to create dynamic modals, please refer to our [Trongate MX documentation](../../trongate_mx).  From there, you'll be able to view an entire section on the subject of [Building Dynamic Modals](../../trongate_mx/0050UI_Enhancements/0079building_dynamic_modals.md).


### Button Container Behavior


Button containers automatically adjust their layout on mobile:

```css
@media screen and (max-width: 550px) {
    p.button-container {
        display: flex;
        flex-direction: column-reverse;
    }
}
```

## Form Elements


Form elements automatically adjust to 100% width of their container while maintaining proper padding and spacing.

Full Name
            
            
            Your Message
```html
<form>
    <label>Full Name</label>
    <input type="text" placeholder="Enter your full name">
    
    <label>Your Message</label>
    <textarea placeholder="Enter your message here..."></textarea>
</form>
```

> [!TIP]
> **Best Practices**
>
> When building responsive layouts with Trongate CSS:
> 
> 
> - Test your interface at the 550px breakpoint to ensure proper adaptation
> - Group related buttons together for proper mobile stacking
> - Utilize the built-in image responsiveness instead of fixed dimensions
> - Consider mobile users when ordering stacked elements


## Summary


Trongate CSS's responsive features provide:


- Single breakpoint simplicity at 550px
- Automatic mobile adaptations for common UI elements
- Responsive form elements and images
- Mobile-optimized modals and button containers

