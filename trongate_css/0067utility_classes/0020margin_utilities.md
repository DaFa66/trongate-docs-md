# Margin Utilities


Trongate CSS provides utility classes for controlling margins. These classes follow a simple naming convention where the first letter indicates the margin direction (t, b, l, r for top, bottom, left, right) and the number indicates the size in em units.

## Margin Direction Classes


There are four types of margin utilities available:


- `mt-{n}` - Sets margin-top
- `mb-{n}` - Sets margin-bottom
- `ml-{n}` - Sets margin-left
- `mr-{n}` - Sets margin-right


Where {n} can be 0 through 7, representing the size in em units.

## Top and Bottom Margins


Here's a demonstration of top margin (`mt-`) and bottom margin (`mb-`) utilities:

Default spacing
mt-3 adds 3em top margin
mt-5 adds 5em top margin
```html
<div>Default spacing</div>
<div class="mt-3">mt-3 adds 3em top margin</div>
<div class="mt-5">mt-5 adds 5em top margin</div>
```

## Left and Right Margins


Here's how to use left margin (`ml-`) and right margin (`mr-`) utilities:

Base ButtonWith ml-2With ml-4
```html
<div class="flex-row">
    <button>Base Button</button>
    <button class="ml-2">With ml-2</button>
    <button class="ml-4">With ml-4</button>
</div>
```

## Common Use Cases


Margin utilities are particularly useful for:

### Blog Post Example


This paragraph has a 2em bottom margin.

#### Subheading with 1em bottom margin


Another paragraph with 3em bottom margin.

CancelSubmit
```html
<h3>Blog Post Example</h3>
<p class="mb-2">This paragraph has a 2em bottom margin.</p>
<h4 class="mb-1">Subheading with 1em bottom margin</h4>
<p class="mb-3">Another paragraph with 3em bottom margin.</p>
<div class="flex-row">
    <button class="alt">Cancel</button>
    <button class="ml-2">Submit</button>
</div>
```

## Available Sizes


Each margin utility class is available in these sizes:


- `*-0` - Removes margin (sets to 0)
- `*-1` through `*-7` - Sets margin to 1em through 7em respectively

## Removing Margins


Use the zero value to remove margins when needed:

No Vertical Margins
```html
<button class="mt-0 mb-0">No Vertical Margins</button>
```

> [!NOTE]
> **Just To Let You Know...**
>
> Margin utilities can be combined to control spacing in multiple directions. For example, `mt-2 mb-3 ml-1` would set different margins for top, bottom, and left respectively.


