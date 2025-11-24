# Custom Routing: An Introduction


**Custom routing** allows you to create clean, intuitive URLs by mapping your desired URL patterns to specific controllers and methods. This feature is particularly useful for creating SEO-friendly URLs and intuitive navigation paths.

## Configuration File


In Trongate, custom routes are defined within 'custom_routing.php'. This file is located in:

```
public/ 
  config/ 
    custom_routing.php
```


From a PHP/framework perspective, custom_routing.php does the following two things:


1. Defines a PHP array named `$routes`.
2. Assigns the value of `$routes` to a PHP constant named `CUSTOM_ROUTES`.

> [!NOTE]
> **Just To Let You Know...**
>
> In normal usage, you (as the developer) will not need to reference the `$routes` array or `CUSTOM_ROUTES` directly after 'custom_routing.php' has been properly set up and saved.



Here is an example of PHP code you might typically find in custom_routing.php:

```php
<?php
$routes = [
    'shop' => 'store/products',
    'shop/shirts' => 'store/category/1',
    'shop/pants' => 'store/category/2'
];

define('CUSTOM_ROUTES', $routes);
```

### An Overview Of How Custom Routing Rules Are Defined


In Trongate, the `$routes` array maps incoming HTTP requests to code. Each item within the array is a key-value pair that defines **a custom routing rule**.


The **key** (i.e., the *left side*) for each rule is **the desired URL pattern** you want to match.


The **value** (i.e., the *right side*) defines **what should be served** when someone visits a URL that matches the left side.


Consider the following line of code from the example above:

```php
'shop' => 'store/products',
```


Here, we are effectively telling Trongate:


*"If someone visits `shop`, please behave as though they had just visited `store/products`."*


Assume the base URL is defined like this:

```php
define('BASE_URL', 'https://trongate.io/');
```

> [!NOTE]
> **Just To Let You Know...**
>
> In Trongate, the `BASE_URL` is defined in 'config.php'. Here is the file location:
> 
> ```
> config/ 
>     config.php
> ```



In this case, a user who navigates to:

```
https://trongate.io/shop
```


...would receive the same response from the website as if they had navigated to:

```
https://trongate.io/store/products
```

> [!TIP]
> **Best Practices**
>
> ### THIS IS REALLY IMPORTANT
> 
> 
> All of the leading PHP frameworks have some kind of custom routing functionality.
> 
> 
> Unfortunately, some developers appear to find the general topic of custom URL routing to be challenging. The main difficulty often comes from confusion about how custom URL routing differs from concepts like URL rewriting.
> 
> 
> Let's clarify the topic at hand.
> 
> ### Don't confuse custom routing with URL rewriting or URL redirecting!
> 
> 
> **Custom routing** determines what content gets served when a user visits a given URL. Custom routing does not change the *actual* URL that appears in the browser's address bar.
> 
> ### Custom Routing vs. URL Rewriting:
> 
> #### Custom Routing
> 
> 
> - In PHP frameworks like Trongate, **custom routing** maps incoming requests (URLs) to specific controllers or actions without altering the visible URL.
> - **URL rewriting**, often handled by the server (e.g., Apache's `.htaccess` or Nginx rules), changes how URLs are processed internally by the server, sometimes hiding implementation details.
> 
> #### Redirecting
> 
> 
> - **Redirecting** sends an HTTP response (e.g., 301, 302) to instruct the browser to navigate to a different URL. This *does* visibly change the address bar.


## In Summary


Custom routing determines what content gets served when a user visits a given URL. It does **not** change the *actual* URL in the browser's address bar.


With Trongate, custom routing is handled via the file 'custom_routing.php'.


Custom routing rules are established by creating a `$routes` array, where each item is a key-value pair:


1. The *keys* represent desired URL paths.
2. The *values* represent what should be served.


Now, let's learn about custom routing patterns...

