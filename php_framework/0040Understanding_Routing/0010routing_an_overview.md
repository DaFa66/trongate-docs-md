# Routing: An Overview


In web development, **routing** is the process of directing incoming web requests to the appropriate code that should handle those requests. Trongate's routing system manages this by mapping URLs (Uniform Resource Locators) to specific modules, controllers, and methods within your application.


Trongate uses a segment-based URL routing approach that creates clean, user-friendly URLs. This is in contrast to traditional PHP applications that often use query strings with symbols like question marks and ampersands.

## Routing Example


Consider a product page on an e-commerce website. Using traditional PHP, you might see a URL like this:

```
https://example.com/store_items.php?id=35
```


With Trongate's routing system, you can create more readable and professional URLs like this:

```
https://example.com/<mark>lenovo-thinkpad</mark>
```


Clean URLs like this offer several benefits:


- They're easier for users to read, understand, and remember
- They look more professional and trustworthy
- They're more friendly for search engine optimization (SEO)
- They hide implementation details of your application


Trongate provides three main ways to handle routing:


1. **Homepage Routing:** Special rules for handling requests to your website's homepage
2. **Automatic Routing:** URLs are automatically mapped to your code based on simple conventions
3. **Custom Routing:** Define your own URL patterns for specific needs


The following pages will explore each of these routing methods in detail, showing you how to create clean, professional URLs for your web applications.

