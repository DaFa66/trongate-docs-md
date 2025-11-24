# Working With Cards


Cards are versatile containers that help organize and present content in a clean, structured way. Trongate CSS provides built-in card styling with minimal markup requirements.

## Basic Card Structure


A basic card consists of two main parts: a heading and a body. Here's a simple example:

Welcome Message
Welcome to our platform! This is a basic card example showing how content can be organized using Trongate's card component.
```html
<div class="card">
    <div class="card-heading">
        Welcome Message
    </div>
    <div class="card-body">
        <p>Welcome to our platform! This is a basic card example showing how content can be organized using Trongate's card component.</p>
    </div>
</div>
```

## Cards with Different Content Types


Cards can contain various types of content including text, lists, buttons, and more:

Product Features
- Responsive Design
- Easy Integration
- Modern Architecture

Learn More
```html
<div class="card">
    <div class="card-heading">
        Product Features
    </div>
    <div class="card-body">
        <ul>
            <li>Responsive Design</li>
            <li>Easy Integration</li>
            <li>Modern Architecture</li>
        </ul>
        <button class="mt-2">Learn More</button>
    </div>
</div>
```

## Multiple Cards Layout


Cards can be arranged side by side using Trongate's flex utilities:

Basic Plan
Perfect for individuals and small teams with a focus on efficiency.

Select Plan
Pro Plan
Ideal for growing businesses and organizations that need more.

Select Plan

In the example, we also use `.text-center` to center-align the modal body content.  Here's the source code:

```html
<div class="flex-row">
    <div class="card" style="width: 48%; margin-right: 2%;">
        <div class="card-heading">
            Basic Plan
        </div>
        <div class="card-body text-center">
            <p>Perfect for individuals and small teams with a focus on efficiency.</p>
            <button class="success">Select Plan</button>
        </div>
    </div>
    <div class="card" style="width: 48%;">
        <div class="card-heading">
            Pro Plan
        </div>
        <div class="card-body text-center">
            <p>Ideal for growing businesses and organizations that need more.</p>
            <button class="primary">Select Plan</button>
        </div>
    </div>
</div>
```

## Customizing Card Appearance


You can customize cards using CSS variables and additional styles:

Custom Styled Card
This card demonstrates custom styling possibilities.
```html
<div class="card custom-card">
    <div class="card-heading">
        Custom Styled Card
    </div>
    <div class="card-body">
        <p>This card demonstrates custom styling possibilities.</p>
    </div>
</div>

<style>
    .custom-card .card-heading {
        background-color: var(--secondary);
        border-color: var(--secondary-dark);
    }
    
    .custom-card .card-body {
        background-color: var(--neutral);
    }
</style>
```

## Top Tips


- Keep card content focused and concise
- Use appropriate spacing within card bodies (utilize margin utility classes)
- Ensure card headings are descriptive but brief
- Consider mobile responsiveness when using multiple cards
- Use consistent card sizes within the same row or section

> [!NOTE]
> **Just To Let You Know...**
>
> Cards automatically inherit your theme's primary color for their headings. You can override this using CSS variables or custom styles as shown in the examples above.


