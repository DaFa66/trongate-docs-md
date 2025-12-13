# Animation Classes


Trongate CSS includes built-in animations for both loading indicators and attention-grabbing effects. These animations help provide visual feedback and draw user attention to important elements.

## Loading Spinner


The loading spinner animation is created using the `.spinner` class. This creates a rotating circular indicator perfect for loading states.


```html
<div class="spinner"></div>
```

### Spinner Variations


The spinner can be aligned differently using additional classes:

#### Left-Aligned Spinner


```html
<div class="spinner spinner-lhs"></div>  <!-- Left-aligned spinner -->
```

#### Center-Aligned Spinner


```html
<div class="spinner"></div>  <!-- Center-aligned spinner (default) -->
```

#### Right-Aligned Spinner


```html
<div class="spinner spinner-rhs"></div>  <!-- Right-aligned spinner -->
```

### Common Use Cases for Spinners


Spinner elements often appear when content is being loaded via Ajax requests.  Often, they'll be used inside [dynamic modal elements](../../trongate_mx/0050UI_Enhancements/0079building_dynamic_modals.md) or [card elements](../0040cards_and_modals/0010working_with_cards.md), like so:

Loading Content
```html
<div class="card">
    <div class="card-heading">Loading Content</div>
    <div class="card-body">
        <div class="spinner"></div>
    </div>
</div>
```

## Customizing Spinners


By default, the spinner uses your primary theme color. However, you can create custom spinners with different colors, sizes, and animation speeds using CSS.

### Different Colors


To change a spinner's color, override the border color in your CSS:


```css
.danger-spinner::after {
    border-color: var(--danger);
    border-right-color: transparent;
    border-top-color: transparent;
}

.success-spinner::after {
    border-color: var(--success);
    border-right-color: transparent;
    border-top-color: transparent;
}

.custom-spinner::after {
    border-color: #9932cc;
    border-right-color: transparent;
    border-top-color: transparent;
}
```

### Custom Sizes and Thicknesses


You can modify the size and border thickness of spinners:


```html
<div class="spinner small-spinner"></div>
<div class="spinner large-spinner"></div>
<div class="spinner thick-spinner"></div>

<style>
    .small-spinner::after {
        width: 16px;
        height: 16px;
        border-width: 2px;
    }
    
    .large-spinner::after {
        width: 48px;
        height: 48px;
        border-width: 4px;
    }
    
    .thick-spinner::after {
        border-width: 6px;
    }
</style>
```

### Animation Speed


Customize the animation speed by modifying the animation duration:


```html
<div class="spinner slow-spinner"></div>
<div class="spinner fast-spinner"></div>

<style>
    .slow-spinner::after {
        animation: spinning 2s infinite linear;
    }
    
    .fast-spinner::after {
        animation: spinning 0.3s infinite linear;
    }
</style>
```

> [!NOTE]
> **Just To Let You Know...**
>
> When customizing spinners, remember to always keep the `border-right-color` and `border-top-color` as `transparent` to maintain the spinning effect. Also, ensure sufficient contrast against your background for visibility.


## Attention Effects


The `.blink` class provides a blinking animation effect to draw attention to important elements.

This text will blink to grab attention

Critical Action Required
```html
<p class="blink">This text will blink to grab attention</p>
<button class="danger blink">Critical Action Required</button>
```

## Combining Effects


Loading and attention effects can be combined with other Trongate CSS classes to create more complex UI patterns:

System Status
Processing Request
```html
<div class="card">
    <div class="card-heading">System Status</div>
    <div class="card-body">
        <div class="flex-row justify-between align-center">
            <span class="blink">Processing Request</span>
            <div class="spinner"></div>
        </div>
    </div>
</div>
```

> [!TIP]
> **Best Practices**
>
> - Use spinners to indicate loading states or processing actions.
> - Apply the blink effect sparingly and only for truly important notifications.
> - Consider accessibility implications when using attention-grabbing animations.
> - Combine with appropriate text to provide context for the animation.
> - Test animations across different browsers to ensure consistent behavior.


## Success & Failure Animations


Trongate MX includes [success animations](../../trongate_mx/0050UI_Enhancements/0076success_animations.md) and [error animations](../../trongate_mx/0050UI_Enhancements/0077error_animations.md), which are automatically rendered after HTTP requests are triggered by Trongate MX.  Click the button below to see a demonstration of how 'success' or 'error' animations respond to user feedback.

Test Feature

Details about how this functionality works is beyond the scope of Trongate CSS documentation.  However, we recommend exploring the [Trongate MX Documentation](../../trongate_mx) for comprehensive details on this feature. In particular, we suggest reviewing the section on [UI Enhancements](../../trongate_mx/0050UI_Enhancements).

