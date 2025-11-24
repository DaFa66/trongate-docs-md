# CSS Variables


Trongate CSS uses CSS custom properties (variables) to maintain consistent styling across your website. These variables control colors, borders, and other visual properties throughout the framework.

## Default Variables


The following variables are defined in Trongate CSS:

```css
:root {
  --primary: #4682b4;
  --primary-dark: #38678f;
  --primary-darker: #294d6b;
  --primary-color: #fff;
  --secondary: #af46b4;
  --border: #c5c5c5;
  --alt: #fff;
  --modal-margin-top: 12vh;
  --success: #4bb446;
  --success-dark: #368532;
  --info: #b2cce1;
  --warning: #b47846;
  --danger: #b4464b;
  --danger-dark: #8f383b;
  --inverse: #333;
  --secondary-dark: #943f99;
  --secondary-darker: #77337a;
  --neutral: #f5f5f5;
}
```

> [!NOTE]
> **Just To Let You Know...**
>
> The variable of `--modal-margin-top` is different from the other CSS variables.  It gets used to declare the top margin of modal windows whereas all of the other variables are used to set color values.


## Default Color Palette


Here are the default color variables that are set within Trongate CSS:

--primary
#4682b4
--primary-dark
#38678f
--primary-darker
#294d6b
--secondary
#af46b4
--secondary-dark
#943f99
--secondary-darker
#77337a
--success
#4bb446
--success-dark
#368532
--info
#b2cce1
--warning
#b47846
--danger
#b4464b
--danger-dark
#8f383b
--inverse
#333
--silver
gradient
--gold
gradient
--neutral
#f5f5f5
--alt
#fff
--border
#c5c5c5
## Understanding the Variables


- 
    `--primary`: Main theme color, typically used for header backgrounds, buttons and interactive elements.
- 
    `--primary-dark`: Slightly darker version of the primary color, used for hover states.
- 
    `--primary-darker`: Darkest version, used for borders and active states.
- 
    `--secondary`: Secondary color for accents and complementary elements.
- 
    `--secondary-dark`: Darker version of the secondary color, used for hover states.
- 
    `--secondary-darker`: Darkest version of secondary color, used for active states.
- 
    `--success`: Green color used to indicate successful actions or positive status.
- 
    `--success-dark`: Darker green for hover states on success elements.
- 
    `--info`: Light blue color used for informational messages.
- 
    `--warning`: Orange color used for warning messages and alerts.
- 
    `--danger`: Red color used for error states and destructive actions.
- 
    `--danger-dark`: Darker red used for hover states on danger elements.
- 
    `--inverse`: Dark contrast color for reversed color schemes.
- 
    `--silver`: Metallic silver color for decorative elements.
- 
    `--gold`: Metallic gold color for premium or featured elements.
- 
    `--neutral`: Base neutral color for backgrounds and default states.
- 
    `--alt`: Alternative neutral color for secondary backgrounds.
- 
    `--border`: Default color for borders and dividers.

## The Primary Color


In addition to the above colors, Trongate CSS has a class named as '.primary-color'.  This class is intened to provide the default font color for a variety of elements including buttons and elements that use the '.primary' background color.

--primary-color (#fff)

The code sample below demonstrates an element that uses the `--primary-color` CSS variable to set the font color of an element.

```html
<div style="padding: 5em; 
     background-color: navy; 
     color: var(--primary-color);">
     The quick brown fox jumps over the lazy dog
</div>
```


And, here's the result:

The quick brown fox jumps over the lazy dog
## Customizing Variables


To override these variables, add your own `:root` declaration after loading Trongate CSS:

```html
<link rel="stylesheet" href="css/trongate.css">

<style>
  :root {
    --primary: #2ecc71;
    --primary-dark: #27ae60;
  }
</style>
```

> [!NOTE]
> **Just To Let You Know...**
>
> Only override the variables you want to change. The others will keep their default values.


## How To Use CSS Variables


Once you've defined your CSS variables, you can use them anywhere within your CSS.  For example, here's how you could apply the `.primary` background color to a footer element.

```css
.footer {
  background-color: var(--primary);
}
```

