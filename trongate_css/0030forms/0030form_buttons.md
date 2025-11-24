# Form Buttons


Trongate CSS provides several button styles and variations that can be used within forms. This guide explores the various button options and their common use cases.

## Basic Buttons


The standard button style is achieved using either the button element or an anchor tag with the `.button` class:

Submit Form[Link Button](#)
```html
<button>Submit Form</button>
<a href="#" class="button">Link Button</a>
```

> [!NOTE]
> **Just To Let You Know...**
>
> Trongate CSS file gives buttons a top margin. The relevant rule is:
> 
> ```css
> button,
> .button {
>   margin: 1em 0.1em 0 0;
> }
> ```
> 
> 
> To mitigate this, a class of `.mt-0` can be added to buttons.  For example:
> 
> ```html
> <button class="mt-0">Submit</button>
> ```


## Alternative Style


Add the `.alt` class to create buttons with an outline style:

Cancel[Back](#)
```html
<button class="alt">Cancel</button>
<a href="#" class="button alt">Back</a>
```

## Status Buttons


Trongate CSS provides contextual button styles for different actions and states:

Confirm ActionProceed with CautionDelete ItemCancel Action
```html
<button class="success">Confirm Action</button>
<button class="warning">Proceed with Caution</button>
<button class="danger">Delete Item</button>
<button class="inverse">Cancel Action</button>
```

## Button Sizes


Buttons can be sized using Trongate's [size classes](documentation/display/trongate_css/utility-classes/size-classes):

Extra SmallSmall ButtonNormal ButtonLarge ButtonExtra Large
```html
<button class="xs">Extra Small</button>
<button class="sm">Small Button</button>
<button>Normal Button</button>
<button class="lg">Large Button</button>
<button class="xl">Extra Large</button>
```

## Form Actions


When positioning multiple buttons at the bottom of a form, consider using `.justify-between` for optimal spacing:

CancelSubmit
```html
<form>
    <input type="text" placeholder="Sample input field">
    <div class="flex-row justify-between">
        <button class="alt mb-0">Cancel</button>
        <button class="mb-0">Submit</button>
    </div>
</form>
```

## Special Button Styles


Trongate CSS includes metallic button styles for emphasis:

Gold ButtonSilver Button
```html
<button class="gold">Gold Button</button>
<button class="silver">Silver Button</button>
```

## Disabled State


Use the disabled attribute to indicate inactive buttons:

Disabled ButtonDisabled Alternative
```html
<button disabled>Disabled Button</button>
<button class="alt" disabled>Disabled Alternative</button>
```

> [!NOTE]
> **Just To Let You Know...**
>
> Disabled buttons maintain their basic styling but have reduced opacity and a "not-allowed" cursor to indicate their inactive state.


