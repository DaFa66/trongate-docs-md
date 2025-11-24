# Cloaking Elements


Trongate CSS provides utility classes to control element visibility and display behavior. These classes are particularly useful for managing content visibility across different states and scenarios.

## The Cloak Class


The `.cloak` class is used to completely hide elements from view. Elements with this class will have `display: none` applied, removing them from the document flow.

This block of code contains three paragraphs.  This is the first paragraph.  It is visible.


This paragraph is hidden with .cloak


This is the third paragraph.  It is also visible.  Notice how the second paragraph is hidden.
```html
<div>
    <p>This block of code contains three paragraphs.  This is the first paragraph.  It is visible.</p>
    <p class="cloak">This paragraph is hidden with .cloak</p>
    <p>This is the third paragraph.  It is also visible.  Notice how the second paragraph is hidden.</p>
</div>
```

### Common Use Cases


The `.cloak` class is particularly useful in the following scenarios:


- Hiding elements that should only be visible under certain conditions (e.g., after user interaction)
- Managing form elements that should appear/disappear based on other selections
- Creating templates where certain elements should be hidden by default

## Dynamic Display Example


Below is an example of how the `.cloak` class might be used in a practical scenario with a toggle button:

Toggle ContentThis content can be toggled visible/hidden
```html
<button onclick="toggleContent()" class="mb-0">Toggle Content</button>
<div id="toggleableContent" class="cloak mt-1">
    <p class="mb-0">This content can be toggled visible/hidden</p>
</div>

<script>
function toggleContent() {
    const content = document.getElementById('toggleableContent');
    content.classList.toggle('cloak');
}
</script>
```

## Form Field Example


Here's a practical example showing how the `.cloak` class can be used to manage conditional form fields:

Ship to different address
        Shipping AddressShipping City
```html
<label>
    <input type="checkbox" onchange="toggleShipping()" class="mt-0"> Ship to different address
</label>

<div id="shippingFields" class="cloak">
    <label>Shipping Address</label>
    <input type="text" placeholder="Enter shipping address">
    
    <label>Shipping City</label>
    <input type="text" placeholder="Enter city">
</div>

<script>
function toggleShipping() {
    const fields = document.getElementById('shippingFields');
    fields.classList.toggle('cloak');
}
</script>
```

> [!NOTE]
> **Just To Let You Know...**
>
> The `.cloak` class is different from setting `visibility: hidden` or `opacity: 0`. While those properties would hide elements visually, `.cloak` completely removes the element from layout flow, ensuring no space is reserved for it.


## Best Practices


When using display utilities, keep these guidelines in mind:


- Use `.cloak` when you want to completely remove an element from both view and document flow
- Consider accessibility implications when hiding content - ensure that important content isn't hidden from screen readers if it needs to be accessible
- Combine with other utility classes (like margin utilities) when managing spacing around toggleable content
- Use meaningful ID names for toggleable elements to maintain clear JavaScript interactions

## Other Cloaking Techniques


The Trongate ecosystem gives developers access to other cloaking techniques, beyond the `.cloak` class.

### Modals


One commonly used example of a situation where an element is cloaked upon initial page load is when dealing with modals.  For example:

Click Me!
Example Modal
×
I'm a modal element.  My source code is hard-coded into the webpage that you are currently viewing.  However, I am hidden when the page initially loads.


Close Modal
```html
<div class="modal" id="example-modal" style="display: none">
    <div class="modal-heading flex-row align-center justify-between">
        <div>Example Modal</div>
        <div onclick="closeModal()">&times;</div>
    </div>
    <div class="modal-body">
        <p class="text-left">I'm a modal element.  My source code is hard-coded into the webpage that you are currently viewing.  However, I am hidden when the page initially loads.</p>
        <p class="text-center">
            <button class="alt" onclick="closeModal()">Close Modal</button>
        </p>
    </div>
</div>

<style>
.modal-heading > div:nth-child(2) {
    cursor: pointer;
}
</style>
```

> [!TIP]
> **Best Practices**
>
> For more information about this, please refer to our section on [Working With Modals](documentation/display/trongate_css/cards-and-modals/working-with-modals).


### Loading Indicators


Trongate CSS also contains a class named as `.mx-indicator`.  This class gets used by Trongate MX to hide an element by default but to then *display* the element as a loading indicator during the HTTP request.


Click the button below to see a loading indicator in action:

Fetch Data
```html
<button mx-get="api/fetch_info" 
        mx-target="#result" 
        mx-indicator="#loading" 
        mx-target-loading="cloak">Fetch Data</button>

<div id="loading" class="spinner mx-indicator"></div>
<div id="result"></div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> In order for the code above to work with *your* application, you'll have to set up and API endpoint and also load Trongate MX onto your webpage.
> 
> 
>     
> For the purposes of avoiding repetition, we won't cover that here.  However, if you are interested in learning more about Trongate's powerful front-end framework, we strongly encourage you to check out the [Trongate MX Documentation](documentation/display/trongate_mx).


