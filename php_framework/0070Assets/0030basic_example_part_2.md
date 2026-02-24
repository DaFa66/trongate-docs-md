# Basic Example - Part 2

## Create an Assets Directory


Within the 'welcome' module, alongside the existing 'controllers' and 'views' directories, create a new directory named 'assets'.


Inside the 'assets' directory, create a subdirectory named 'js'. This 'js' directory will serve as the repository for JavaScript files within the module.

## Create a JavaScript File


Next, create a JavaScript file named 'ahoy.js' that contains a single line of code: an alert command.

```php
alert("JavaScript alert!");
```


Save the 'ahoy.js' file inside the 'js' directory located within 'assets'.



    ![The contents of a basic Trongate web application](https://dafadev.net/a1/images/79/_left_siCTKy.png)
    
*Directory structure screenshot*


## Calling the JavaScript File


To include the JavaScript file in the 'hello' view file, use standard 'script' tags with the 'src' attribute set to = htmlspecialchars("'welcome_module/js/ahoy.js'") ?>. For example:

```php
<?= htmlspecialchars('<script src="welcome_module/js/ahoy.js"></script>') ?>
```

## View File with JavaScript Integration


Below is the complete code for the 'hello' view file, incorporating the 'script' tags just before the closing body tag:

```html
<!DOCTYPE html>  
<html lang="en">  
  <head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>Document</title>  
  </head>  
  <body>  
    <h1>Hello World</h1>  
    <script src="welcome_module/js/ahoy.js"></script>  
  </body>  
</html>
```

## Testing the JavaScript File


Save the file and refresh the page in the browser. If a JavaScript alert box appears, it confirms that the JavaScript file has loaded successfully.



    ![browser screenshot](https://dafadev.net/a1/images/79/_javascr327M.png)
    
*Screenshot taken from the URL, <base-url>welcome/hello*


> [!NOTE]
> **Just To Let You Know...**
>
> The integration of a JavaScript file into a module containing PHP files marks a significant milestone. This capability enhances productivity by enabling the development of sophisticated, self-contained modules without reliance on third-party libraries.
> 
> 
> In this example, a JavaScript file was included within the module. However, the same approach can be applied to incorporate images, PDFs, CSS files, or other non-PHP resources.


