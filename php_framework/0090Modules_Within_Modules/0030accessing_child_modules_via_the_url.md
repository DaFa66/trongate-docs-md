# Accessing Child Modules Via The URL


The process of accessing parent modules - either via the URL or via other modules - is entirely unchanged. So, nothing new to learn there! Just access your parent modules the way you would normally access any normal Trongate modules.


Child Modules are a little different.


To access child modules via the URL, prefix the first segment of the URL with the name of the parent module followed by a hyphen. For example, let's assume that we want to access our *accessories* child module. More specifically, let's assume that we'd like to invoke the 'display()' method. We could invoke this by navigating to the URL:


**http://localhost/app_name/cars-accessories/display**


This would, of course, be assuming that 'accessories' is inside a parent module called 'cars'.

## Creating Links


To create a text link that invokes the display() method, inside accessories, we could use the following code:

```php
<?= anchor("cars-accessories/display", "view accessories") ?>
```


Again, notice how the first segment of the URL contains the parent module (in this case, 'cars') followed by a hyphen.

