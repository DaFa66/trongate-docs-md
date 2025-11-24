# Out-of-Band Swaps


Have you ever wanted to update several different parts of your webpage with a single request? That's exactly what Trongate MX's out-of-band swaps let you do, using the `mx-select-oob` attribute. Let's explore how it works.

## What Are Out-of-Band Swaps?


Imagine you're redecorating a room. Your main focus might be replacing the sofa, but while you're at it, you might want to update the curtains and swap out some cushions too. That's what out-of-band swaps do for your webpage - they let you update multiple elements in one go, even if they're in different places on the page.

## Two Ways to Write Your Swaps

### 1. The Simple Way: Using Lists


This is like writing a shopping list. You simply write what you want to get from the server and where you want to put it, separated by colons:

```
mx-select-oob="#server-content:#page-location, .server-title:.page-title"
```


Each pair works like this:


- **Before the colon:** What you want to grab from the server's response
- **After the colon:** Where you want to put it on your current page

### 2. The Detailed Way: Using JSON


This method gives you more control, letting you specify exactly how you want to insert your content:

```
mx-select-oob='[
    {"select": "#server-content", "target": "#page-location", "swap": "innerHTML"},
    {"select": ".server-title", "target": ".page-title", "swap": "outerHTML"}
]'
```

## A Real-World Example


Let's say you're building a dashboard that needs to update several areas at once. The code below shows how you could do this using Trongate's form_button() function:

```vf
<?php
$attributes = [
    'mx-get' => 'dashboard/refresh',
    'mx-select' => '#main-content',
    'mx-select-oob' => '#notifications:#alert-area, #user-stats:#sidebar-stats, #activity-feed:#recent-activities'
];

echo form_button('refresh_btn', 'Refresh Dashboard', $attributes);
?>

<div id="dashboard">
    <div id="alert-area"></div>
    <div id="sidebar-stats"></div>
    <div id="main-content"></div>
    <div id="recent-activities"></div>
</div>
```


Here's how the same result can be achieved with pure HTML:

```html
<button mx-get="dashboard/refresh"
        mx-select="#main-content"
        mx-select-oob="#notifications:#alert-area, #user-stats:#sidebar-stats, #activity-feed:#recent-activities">
    Refresh Dashboard
</button>

<div id="dashboard">
    <div id="alert-area"></div>
    <div id="sidebar-stats"></div>
    <div id="main-content"></div>
    <div id="recent-activities"></div>
</div>
```

## Cleaner Syntax Using JSON


Take another look at the code samples above.  You'll surely have noticed that the code pertaining to `mx-select-oob` is cumbersome and slightly messy.  The good news is, you can make your code much cleaner by combining Trongate's form_button() function with some JSON encoding.


Here's how it's done:

```vf
<?php 
$oob_swaps = [
    [
        'select' => '#notifications',
        'target' => '#alert-area'
    ],
    [
        'select' => '#user-stats',
        'target' => '#sidebar-stats'
    ],
    [
        'select' => '#activity-feed',
        'target' => '#recent-activities'
    ]
];

$attributes = [
    'mx-get' => 'dashboard/refresh',
    'mx-select' => '#main-content',
    'mx-select-oob' => json_encode($oob_swaps)
];

echo form_button('refresh_btn', 'Refresh Dashboard', $attributes);
?>
```


That's much neater, right?


The trick is to use `json_encode()` - a PHP function that comes as part of the PHP language.  You can learn more about the 'json_encode' function [here](https://www.php.net/manual/en/function.json-encode.php).


For those who prefer to write using pure HTML, we've got you covered!  Here's your alternative syntax:

```html
<button mx-get="dashboard/refresh"
        mx-select="#main-content"
        mx-select-oob='[
            {"select": "#notifications", "target": "#alert-area"},
            {"select": "#user-stats", "target": "#sidebar-stats"},
            {"select": "#activity-feed", "target": "#recent-activities"}
        ]'>
    Refresh Dashboard
</button>
```

> [!TIP]
> **Best Practices**
>
> Think of your selectors like addresses. The more specific they are, the more certainty you have that your content will end up exactly where you want it.


## Using OOB Swaps Without a Main Target


Sometimes you might want to update multiple elements with OOB swaps without updating any main content. In this case, you can use `mx-target="none"` to indicate that no primary content should be updated, while still allowing OOB swaps to occur.


This is particularly useful for polling scenarios where you want to update multiple elements on a regular basis:

```html
<div id="stats-container" 
     mx-get="api/stats_update" 
     mx-target="none" 
     mx-select-oob='[
         {"select": ".current-visitors", "target": "#visitor-count"},
         {"select": ".server-status", "target": "#status-indicator"}
     ]'>
    <!-- This container won't be updated directly -->
</div>
```


With this setup, the API would return HTML fragments like:

```
<div class="current-visitors">157 visitors online</div>
<div class="server-status">All systems operational</div>
```


When the response is received, Trongate MX will find the elements matching `.current-visitors` and `.server-status` in the response, and update the corresponding target elements on your page, without updating the container element itself.

## Top Tips


- Use clear, specific IDs and classes that describe what the element contains
- Keep your selectors as simple as possible while still being unique
- Test your swaps with different types of content to ensure they work as expected
- Remember that your server response needs to include all the elements you're trying to select

## Summary


Out-of-band swaps are your secret weapon for creating smooth, efficient page updates. Instead of making multiple requests or reloading the entire page, you can update exactly what you need, where you need it, all in one go. Whether you choose the simple list approach or the more detailed JSON method, you now have the power to create more dynamic and responsive web applications.

