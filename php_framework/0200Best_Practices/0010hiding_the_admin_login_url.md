# Hiding The Admin Login URL


The default admin login URL for Trongate websites is made up of a base URL followed by **trongate_administrators/login**. However, a base URL followed by **tg-admin** will also work. This shorter URL is made possible by the custom_routing.php file, which is inside the config directory.


If somebody tried to hack into your admin panel then you can be sure that they would focus on entry points such as your default admin login and the URL for receiving post requests from your admin login. Of course, if a malicious user knows your login URL for your admin panel then it does not mean that they have successfully hacked your site. It merely means that they have a good starting point to carry out their diabolical deeds.


With this in mind, it's a good practice to make your login URL secret and - hopefully - impossible to guess. Doing this is would make life much more difficult for a would-be hacker.

## How To Create A Secret Admin Login URL


**STEP 1: Think of a word that is difficult to guess but meaningful and easy to remember for the site owner.**


This could be an entirely made-up word or a word that's made of a combination of two words. Avoid spaces or any unusual characters. For the moment, let's assume that our secret word is going to be **fantasticola**. This means that to log into our site admin panel, the URL should be:


The base URL, followed by 'fantasticola', e.g., example.com/fantasticola


**STEP 2: Modify custom_routing.php **


The next step is to modify your custom_routing.php file, which is inside your config directory. Simply replace all instances of 'tg-admin' with 'fantasticola' (or whatever your secret world may be).


For example, here's some sample code from custom_routing.php:

```php
<?php
$routes = [
  "tg-admin" => "trongate_administrators/login",
  "tg-admin/submit_login" => "trongate_administrators/submit_login"
];

define("CUSTOM_ROUTES", $routes);
```


The code above would be changed to:

```php
<?php
$routes = [
  "fantasticola" => "trongate_administrators/login",
  "fantasticola/submit_login" => "trongate_administrators/submit_login"
];

define("CUSTOM_ROUTES", $routes);
```


**Step 3: Modify and uncomment the secret login declaration on 'Trongate_administrators.php'**


Finally, open up Trongate_administrators.php. If you are using version 1.3.3031 or higher then around line 5 could should see the following code:

```php
//private $secret_login_segment = "tg-admin";
```


Uncomment this line and change the secret login segment to your chosen word. For example:

```php
private $secret_login_segment = "fantasticola";
```


**That's it!**


If you have followed these instructions and you are using Trongate version 1.3.3031 or higher then the trongate_administrators/login page will produce a 404 error. In order to access your admin login URL, users would have to go to your base URL followed by your secret word.

