# Custom Routing Patterns


As discussed [previously](documentation/display/php_framework/understanding-routing/introducing-custom-url-routing), custom routing is handled via the initialization of a `$routes` array within the file, 'custom_routing.php'.

```
config/ 
    custom_routing.php
```


Trongate offers two types of routing patterns that can be used to set up custom routing rules. These are:


1. Basic Routing Patterns
2. Dynamic Routing Patterns


---

## Basic Routing Patterns


**Basic routing patterns** are static mappings. A basic routing pattern is designed to match an explicitly declared URL path to an explicitly defined response.


The matching process for these routes involves checking if the current URL matches one of the keys in the `$routes` array. If a match is found, the framework directs the request to the corresponding controller and method specified by the value of that key.

> [!NOTE]
> **Just To Let You Know...**
>
> When Trongate is attempting to match URLs, the `BASE_URL` will be disregarded.


### Basic Custom Routing Example


To create a basic custom routing rule, add a key-value pair to the `$routes` array.  Here's an example:

```php
<?php
$routes = [
    'login' => 'users/login'
];

define('CUSTOM_ROUTES', $routes);
```


With the code above, any request made to `<base-url>login`, will cause the following chain of events to occur:


- The framework will attempt to locate a module named 'users'.
- The framework will attempt to find a controller file, named 'Users.php' within the users module.
- The framework will attempt to find and load a PHP class named 'Users', within the target controller file.
- The framework will attempt to find a method named `login()`, within the Users class.
- The framework will attempt to invoke the target `login()` method.


Put simply, if somebody was to go to:

```
http://example.com/login
```


...the address bar would **not** change but the website would behave as though the user had navigated to:

```
http://example.com/users/login
```

### A Word Of Caution


Basic custom routing offers an easy way to effectively declare:


*"If a user arrives on 'x', behave as though they have arrived on 'y'."*


**But beware!**


Basic custom routing *only* works when the current URL can be **precisely** matched to the defined URL pattern.  It should never be used to *generally* swap 'x' for 'y' across a range of URLs.

> [!CAUTION]
> Suppose you'd like to have the following rule enforced:
> 
> 
> *"When a user lands on **any** URL with a first segment of 'nice-segment', respond as though they have landed on an equivalent URL, but with a first segment of 'ugly_segment'."*
> 
> 
> It might seem tempting to set up a simple custom URL routing rule like this:
> 
> ```php
> 'nice-segment' => 'ugly_segment'
> ```
> 
> 
> However, this would be a blunder since basic custom routing patterns only work for **exact** matches.
> 
> 
> The rule above would not account for any variations in the URL beyond the first segment. So, it's possible that the current URL could include additional segments *beyond* the first segment.  Those kinds of URLs wouldn't be properly routed without a dynamic match.
> 
> 
> The correct way to define such a rule would be:
> 
> ```php
> 'nice-segment/(:all)' => 'ugly_segment/$all'
> ```
> 
> 
> This would be a *dynamic* routing pattern - which happens to be the topic of discussion for the remainder of this page.



---

## Dynamic Routing Patterns


Dynamic routing patterns allow for more flexible routing by capturing variable segments in the URL. They use **wildcard placeholders** to match specific parts of the URL and pass those values to the controller method. This feature is essential when the URL structure involves dynamic parameters, such as IDs, names, or multi-segment paths.

## Wildcard Types


Trongate provides three types of wildcards for capturing URL segments:


- **(:num)**: Matches only numeric values. This is useful for routes where you expect a numerical identifier, such as product IDs.
- **(:any)**: Matches any characters except the forward slash ('/'). This is useful for more general segments like categories or user names.
- **(:all)**: Matches all remaining segments in the URL. This wildcard captures everything following it, which is helpful for paths with multiple segments (e.g., documentation paths or multi-level categories).


Here's an example of how these wildcards can be used:

```php
<?php
$routes = [
  // Match numeric IDs
  'product/(:num)' => 'store/item/$1',  // Matches product/123
    
  // Match any segment
  'category/(:any)' => 'store/category/$1',  // Matches category/t-shirts
    
  // Multiple wildcards
  'blog/(:any)/(:num)' => 'blog/post/$1/$2',  // Matches blog/summer/2024
    
  // Match all remaining segments
  'help/(:all)' => 'help/$all'  // Matches help/docs/api/v2
];
?>
```

## Wildcard Table


| Pattern | Matches | Example |
| ---|---|---|
| `(:num)` | Numbers only | 123 |
| `(:any)` | Any characters except '/' (the forwardslash) | user-1 |
| `(:all)` | Captures all remaining segments | docs/api/v2 |

> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** The `(:all)` wildcard must be the last segment in your route pattern as it captures everything that follows.


## Controller Mapping


The right side of each route maps to a controller and method, and the placeholders from the left side are passed to the method as parameters. Here's an example of how it works:

```php
<?php
$routes = [
  'url-path' => 'controller/method'
];

// Examples
$routes = [
  'products' => 'store/list',               // Store::list()
  'product/(:num)' => 'store/view/$1',      // Store::view($id)
  'docs/(:all)' => 'documentation/$all',    // Captures full path
  'search' => 'store/search'                // Store::search()
];
?>
```


In the example above, `(:num)` captures the numeric ID passed in the URL, and `(:any)` captures any string-based segment. The `(:all)` wildcard is used for capturing everything after a particular path segment.

## Route Groups


Organizing your routes into groups makes the routing system more maintainable and readable. Here's an example of how to group related routes together:

```php
<?php
$routes = [
  // Product routes
  'products' => 'store/list',
  'products/new' => 'store/new_items',
  'products/sale' => 'store/sale_items',
    
  // Category routes
  'category/(:any)' => 'store/category/$1',
  'categories' => 'store/all_categories',
    
  // Documentation routes
  'docs/(:all)' => 'documentation/$all',
    
  // Cart routes
  'cart' => 'cart/view',
  'cart/add/(:num)' => 'cart/add/$1',
  'cart/remove/(:num)' => 'cart/remove/$1'
];
?>
```

## Important Considerations

> [!NOTE]
> **Just To Let You Know...**
>
> **Important:** Routes are matched in order of specificity. More specific routes should be placed before more general ones, especially before routes using `(:all)`.


## Best Practices

> [!TIP]
> **Best Practices**
>
> - Keep URLs clean and meaningful
> - Use consistent naming patterns
> - Place more specific routes first
> - Group related routes together
> - Use appropriate wildcards for dynamic segments
> - Use `(:all)` when you need to capture multiple segments in a single route


