# Selecting Content


The `mx-select` attribute in Trongate MX is a powerful feature that allows you to extract and use specific parts of a server response, rather than the entire response. This capability is particularly useful when dealing with large HTML documents where only a portion of the content is needed.

## Understanding mx-select


When you use `mx-select`, you're telling Trongate MX to look inside the server's response and pick out only the parts you've specified. This is done using CSS selector syntax, allowing for precise targeting of elements within the response.

## When to Use mx-select


The `mx-select` attribute is particularly useful in scenarios where:


- You're fetching data from an endpoint that returns an entire HTML page, but you only need a specific section.
- You want to update part of your page without affecting the rest of the layout.
- You're working with legacy systems or APIs that return full pages instead of focused data.

## Example Scenario


Let's consider a practical example to illustrate the use of `mx-select`:


Imagine having an API that returns a complete HTML page but you only need one element from it (like a specific table).  With `mx-select` you can fetch ***just that element*** and add it onto your current page. Here's how:

```html
<button mx-get="api/full_page_data" 
        mx-target="#data-container" 
        mx-select="table#user-data">Fetch Data</button>

<div id="data-container">
    <!-- The selected table will be inserted here -->
</div>
```


In the example above, we're fetching a `<table>` element - from a target endpoint.  The target HTML table (i.e., the table that we are *fetching*) has an 'id' of 'user-data'.  Once the table has been fetched, it would then being inserted inside our `<div>` element that has an id of 'data-container'.


Here's an alternative way to build the same solution, using Trongate's form_button() form helper function:

```vf
<?php
$btn_attr = [
    'mx-get' => 'api/full_page_data',
    'mx-target' => '#data-container',
    'mx-select' => 'table.important-data'
];
echo form_button('fetch_btn', 'Fetch Data', $btn_attr);
?>

<div id="data-container">
    <!-- The selected table will be inserted here -->
</div>
```

### Breaking Down the Example


- The button triggers a GET request to 'api/full_page_data', which returns a complete HTML page.
- `mx-select="table#user-data"` instructs Trongate MX to extract only the table with the id of 'user-data' from the response.
- The selected table is then inserted into the #data-container div.

## Benefits of Using mx-select


This approach offers several advantages:


- **Reusability:** You can reuse existing server-side rendering logic that generates full pages.
- **Performance:** By minimizing the amount of data inserted into the DOM, you can improve page performance.
- **Clean Markup:** Your client-side markup remains clean and focused on the required data.
- **Flexibility:** You can easily change what part of the response you want without modifying server-side code.

## Advanced Usage


The `mx-select` attribute is not limited to simple selectors. You can use complex CSS selectors to pinpoint exactly what you need:

```vf
<?php
$btn_attr = [
    'mx-get' => 'api/complex_data',
    'mx-target' => '#specific-data',
    'mx-select' => 'main > div.data-section:nth-child(2) table'
];
echo form_button('fetch_btn', 'Fetch Specific Table', $btn_attr);
?>
```


The example above selects a `<table>` element that is the second child of a `<div>` with class 'data-section', which is inside the  `<main>` element.


Below is the solution, written with pure HTML:

```html
<button mx-get="api/complex_data" 
        mx-target="#specific-data" 
        mx-select="main > div.data-section:nth-child(2) table">
        Fetch Specific Table</button>

<div id="specific-data"></div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** The `mx-select` attribute uses CSS selector syntax. You can use any valid CSS selector to pinpoint the exact element you need from the response. This includes IDs, classes, attributes, and even pseudo-selectors.


> [!TIP]
> **Best Practices**
>
> - Use specific and unique selectors to ensure you're getting exactly what you need.
> - Consider the structure of your server responses when designing your selectors.
> - Test your selectors thoroughly, especially when working with dynamic content.


