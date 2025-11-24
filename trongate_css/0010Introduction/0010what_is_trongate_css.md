# What is Trongate CSS?


Trongate CSS is a lightweight CSS library designed to make plain HTML visually appealing with minimal effort. Unlike other CSS frameworks that require extensive usage of utility classes or component structures, Trongate CSS enhances standard HTML elements automatically, providing a seamless and elegant experience.

## Do We Really Need Another CSS Library?


With the plethora of CSS libraries and frameworks available, it's natural to ask, "**do we *really* need Trongate CSS?**":


The answer is simple: **you don't have to use it.**


Trongate CSS is entirely optional and works independently of the Trongate PHP framework. If you already have a CSS library or framework that suits your needs, you can continue using it alongside Trongate CSS - or not at all. The choice is yours.


While many CSS libraries are excellent, some come with significant challenges.  For instance:


1. 
    **Rewrite culture**: Many of the world's most popular CSS frameworks are subjected to ruthless rewrite and reversioning schedules ***with breaking changes***. Astonishingly, the makers of some of these *other* CSS frameworks appear to be proud of their ongoing endeavours to break their own intellectual assets. Rewrite culture is a huge problem across the CSS landscape and - sadly - it has [ruined](https://www.yiiframework.com/extension/yiisoft/yii2-bootstrap4/doc/guide/2.0/en/migrating-yii2-bootstrap) many good PHP projects.
  
2. 
    **Steep learning curves**: Modern CSS frameworks often introduce a labyrinth of utility classes, configuration files, and dependencies. This forces developers to spend hours, if not days, poring over exhaustive documentation just to accomplish what should be straightforward tasks. For instance, creating a responsive layout might require mastery of grid systems, flex utilities, and component-based styling approaches. Instead of speeding up development, these frameworks can make it feel like you're taking a crash course in a new programming language.
  
3. 
    **Bloated code**: Many CSS frameworks bundle an overwhelming array of pre-built components, styles, and utilities, most of which are irrelevant to your project. This can lead to unnecessarily large CSS files, slowing down page load times and bloating your source code. Even worse, developers often include the entire framework rather than just the parts they need, adding kilobytes - or even megabytes - of unused styles to their projects. The result is wasted bandwidth and poorer performance for end users.
  
4. 
    **Framework lock-in**: Dependency on framework-specific classes often leads to a scenario known as "framework lock-in," where your entire project becomes tethered to the quirks and updates of a particular library. Over time, this can make migrating to another framework - or even updating to a new version of the same framework - a monumental task. Designs that once felt modern can become outdated overnight, requiring extensive rework to achieve compatibility. For developers, this can mean a choice between starting from scratch or enduring endless frustration.
  

> [!NOTE]
> **Just To Let You Know...**
>
> Consider this simple HTML code:
> 
> ```html
> &lt;button&gt;Click Me&lt;/button&gt;
> ```
> 
> 
> With most CSS frameworks, styling this button would require multiple classes:
> 
> ```
> &lt;button class="btn btn-primary px-4 py-2 rounded"&gt;Click Me&lt;/button&gt;
> ```
> 
> 
> With Trongate CSS, the basic HTML element is all you need - it's beautifully styled by default!


## Key Features


- **Zero-class styling**: Automatically styles basic HTML elements.
- **Mobile-first design**: Responsiveness without extra classes.
- **Lightweight**: Small file size with no dependencies.
- **Modern defaults**: Contemporary styling out of the box.
- **Framework agnostic**: Compatible with any JavaScript framework or none at all.

## How It's Different

> [!TIP]
> **Best Practices**
>
> - **No classes required**: Unlike Bootstrap or Tailwind, basic elements are styled without additional classes.
> - **Minimal learning curve**: Familiarity with HTML is all you need to get started.
> - **Pure simplicity**: Focus on content, not styling classes.
> - **Fast development**: Build professional web pages quickly and efficiently.


### Example: Form Styling Comparison


Here's how Trongate CSS simplifies form development compared to other frameworks:

```html
<!-- Traditional Framework -->
&lt;form class="form-container p-4 border rounded"&gt;
    &lt;div class="form-group mb-3"&gt;
        &lt;label class="form-label"&gt;Name&lt;/label&gt;
        &lt;input type="text" class="form-control"&gt;
    &lt;/div&gt;
&lt;/form&gt;

<!-- Trongate CSS -->
&lt;form&gt;
    &lt;label&gt;Name&lt;/label&gt;
    &lt;input type="text"&gt;
&lt;/form&gt;
```

## Conclusion


Think of Trongate CSS as being a patch (or, if you prefer, a *fix*) for **pure HTML**.


Here's three huge benefits that Trongate CSS brings to the table:


1. There's not much to learn!  Trongate CSS makes pure HTML look beautiful.
2. Trongate CSS encourages developers to write **pure HTML** - thereby giving projects massive degrees of stability.
3. Since Trongate CSS is very lightweight and produces beautiful source code, it makes websites built with Trongate CSS very attractive to search engines like Google.

