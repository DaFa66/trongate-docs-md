# Size Classes


Trongate CSS provides utility classes for adjusting sizes. These classes scale elements relative to their base size using em units.

## Available Size Classes


There are four size modifier classes available:


1. `.xl`
2. `.lg`
3. `.sm`
4. `.xs`


The code below shows the effect that these classes have upon text.

Extra Large Text (.xl)


Large Text (.lg)


Default Text Size (no class)


Small Text (.sm)


Extra Small Text (.xs)
```html
<p class="xl">Extra Large Text (.xl)</p>
<p class="lg">Large Text (.lg)</p>
<p>Default Text Size (no class)</p>
<p class="sm">Small Text (.sm)</p>
<p class="xs">Extra Small Text (.xs)</p>
```

## Using Size Classes with Buttons


Size classes can be applied to buttons to create clear visual hierarchies in your interfaces:

Extra Large ButtonLarge ButtonNormal ButtonSmall ButtonExtra Small Button
```html
<button class="xl">Extra Large Button</button>
<button class="lg">Large Button</button>
<button>Normal Button</button>
<button class="sm">Small Button</button>
<button class="xs">Extra Small Button</button>
```

> [!TIP]
> **Best Practices**
>
> For more on this, check out our documentation on [Form Buttons](../0030forms/0030form_buttons.md).


## Practical Applications


Size classes can effectively establish content hierarchy. Here's an example showing different size classes working together in [card element](../0040cards_and_modals/0010working_with_cards.md):

Product Features
### Premium Package


Main description of the product goes here.


- Feature One
- Feature Two


Terms and conditions apply. See details below.


*Prices may vary by region
```html
<div class="card">
    <div class="card-heading">
        Product Features
    </div>
    <div class="card-body">
        <h3 class="lg">Premium Package</h3>
        <p>Main description of the product goes here.</p>
        <ul>
            <li>Feature One</li>
            <li>Feature Two</li>
        </ul>
        <p class="sm">Terms and conditions apply. See details below.</p>
        <p class="xs">*Prices may vary by region</p>
    </div>
</div>
```

## Size Class Specifications


The size classes use the following scale:


- `.xl` - Sets size to 1.5em (150% of base size)
- `.lg` - Sets size to 1.3em (130% of base size)
- `.sm` - Sets size to 0.85em (85% of base size)
- `.xs` - Sets size to 0.7em (70% of base size)

> [!NOTE]
> **Just To Let You Know...**
>
> Size classes can be combined with other utility classes like margin utilities (`mt-1`, `mb-1`, etc.) for more precise control over element presentation.


