# Homepage Routing


The homepage is often the most visited page of any website. Trongate provides a simple way to control what happens when users visit your website's homepage (the root URL of your site).

## Homepage Configuration


Homepage routing in Trongate is controlled through three constants in your `config.php` file, which is located in the 'config' directory. Here are the default settings:

```php
define('DEFAULT_MODULE', 'welcome');
define('DEFAULT_CONTROLLER', 'Welcome');
define('DEFAULT_METHOD', 'index');
```


These three constants work together to determine what code runs when someone visits your homepage:


- **DEFAULT_MODULE**: The module folder where your code is located
- **DEFAULT_CONTROLLER**: The controller file that contains your code
- **DEFAULT_METHOD**: The specific function that will run


With these default settings, visiting your homepage will:


1. Look inside the 'welcome' module folder
2. Find the 'Welcome' controller file
3. Run the 'index' method inside that controller

> [!NOTE]
> **Just To Let You Know...**
>
> In web development, the URL that maps to the homepage of an application is often referred to as the **base URL**.  In Trongate, the base URL is declared, inside 'config.php', through a [PHP constant](https://www.w3schools.com/php/php_constants.asp) named as `BASE_URL`.  The last character of your base URL should always be a forwardslash.
> 
> 
> Here's the contents of the config.php file that is being used for the this website (yes, really!):
> 
> ```php
> <?php
> define('BASE_URL', 'https://trongate.io/');
> define('ENV', 'live');
> define('DEFAULT_MODULE', 'welcome');
> define('DEFAULT_CONTROLLER', 'Welcome');
> define('DEFAULT_METHOD', 'index');
> define('MODULE_ASSETS_TRIGGER', '_module');
> ```


## Customizing Your Homepage


You can change what appears on your homepage by modifying the constants within config.php.  This file is located in:

```
config/ 
    config.php
```

### Example


For example, if you want your homepage to display a dashboard, you might use:

```php
define('DEFAULT_MODULE', 'dashboard');
define('DEFAULT_CONTROLLER', 'Dashboard');
define('DEFAULT_METHOD', 'index');
```

> [!NOTE]
> **Just To Let You Know...**
>
> **Important:** Before changing these settings, make sure:
> 
> 
> - Your module folder exists
> - Your controller file exists inside the module folder
> - Your method exists inside the controller
> 
> 
> Otherwise, users will see an error when they visit your homepage.


