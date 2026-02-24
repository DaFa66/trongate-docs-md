# Custom Routing - Practical Examples


There may be situations when you'd like to create custom page URLs. For example, let's assume that you own an online shop that sells laptops. A typical URL for a product page might look something like this:

```
https://www.yoursite.com/store_items/display/88
```


Wouldn't it be nice if you could change these types of URLs so that they are:


- More search engine friendly
- Easier for visitors to remember


Custom routing makes this and more possible. Let's go through a few different scenarios and explore how we could use custom routing to create attractive page URLs.


---

## Scenario 1: 'News to Blog'


**Challenge:** You'd like to use a 'news' module from a previous project (we'll call it 'website A') to create a new blog for a second website ('website B').
    However, you don't want the new blog module to contain URLs that start with 'news/'. Instead, you'd like the URLs to start with 'my-blog/'.


**More Info:** Let's assume that the homepage for the 'news' module is:

```
http://yoursite.com/news
```


Typing the URL shown above into the address bar would load the index method for the 'news' module. Your goal might be to load the news module by going to:

```
http://yoursite.com/my-blog
```


**How It's Done:**


- In your text editor, open the file '**custom_routing.php**'. It's inside the '**config**' directory.
- 
        Inside the custom_routing.php file, add a new key-value pair to the `$routes` array where 'my-blog' is assigned to 'news'. For example:
    

```php
<?php
  $routes = [
  'my-blog' => 'news',
  'tg-admin' => 'trongate_administrators/login',
  'tg-admin/submit_login' => 'trongate_administrators/submit_login'
];

define('CUSTOM_ROUTES', $routes);
```


---

## Scenario 2: 'Dealing With Numeric Wildcards'


**Challenge:** You have an online shop that sells laptops. All of the product pages in your online shop have a first segment of 'store_items/'. For example:

```
http://yoursite.com/store_items/display/88
```


You'd like to change the URLs so that instead of the first segment saying 'store_items', the product pages should all have a first segment of 'laptops'. For example:

```
http://yoursite.com/laptops/display/88
```


**How It's Done:**


In custom_routing add the following key-value pair to the $routes array:

```php
'laptops/display/(:num)' => 'store_items/display/$1',
```


---

## Scenario 3: 'Super SEO-friendly URLs'


**Challenge:** Sticking with our online shop example, let's imagine that you'd like to have product pages where all of the URLs are super search engine friendly. So, instead of having a URL like:

```
http://yoursite.com/laptops/display/88
```


Perhaps you would prefer to have a URL like this:

```
http://yoursite.com/laptops/information/macbook
```


This kind of URL could rightfully be considered to be **super search engine friendly**. Having an online shop with those kinds of URLs could be extremely valuable for anyone who had an interest in achieving a high search engine ranking.


**How It's Done:**


The first step to creating a super search engine friendly URL, as described above, would involve giving all of our products a unique 'slug'. In the Trongate Desktop App, this gets called a 'URL column'.

![The Trongate Desktop App](https://dafadev.net/a1/images/choose_ufaFH.gif)
        
*Choosing a URL column*

Having created a unique slug (URL column value) for each product, we would then add the following key-value pair to the $routes array, inside '**custom_routing.php**':

```php
'laptops/information/(:any)' => 'store_items/display/$1',
```


If you can follow the steps above then congratulations! You now know how to build pages that are super search engine friendly and that load approximately twenty times faster than Laravel.
    Best of all, your clients will think you're a genius after they've made it to the top of Google and recommended you to all of their friends!

