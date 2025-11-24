# Basic Example - Part 1


To clearly illustrate the purpose and functionality of the **File Asset Manager**, it is beneficial to examine a practical example. This section will guide through a straightforward example using the 'welcome' module that's included with all Trongate framework installations. The objective is to store a JavaScript file within the 'welcome' module and display a simple webpage that executes the module's internal JavaScript file.

## The Starting Point


A fresh installation of a Trongate web application includes a module named 'welcome', which contains a controller file named **Welcome.php**. The 'Welcome' controller file comprises a class with a single method, as illustrated below:

```php
<?php
class Welcome extends Trongate {

  function index() {
    $this->view("welcome");
  }

}
```

> [!NOTE]
> **Just To Let You Know...**
>
> The precise code contained within the 'Welcome' controller file will differ from the example shown. For brevity, elements such as access modifiers (e.g., public/private/protected), type hinting, return types, and doc blocks have been omitted.


## Adding a New Method


Next, a new method will be added to the controller file. This method, named 'hello', will load a simple view file displaying the message 'hello world'. The updated controller code is as follows:

```php
<?php
class Welcome extends Trongate {

  function index() {
    $this->view("welcome");
  }

  function hello() {
    $this->view("hello");
  }

}
```

## A Simple View File


Proceed by creating a view file containing basic HTML. The code sample below demonstrates a simple HTML template with the message 'Hello World' encapsulated within `<h1>` tags.

```vf
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <h1>Hello World</h1>
</body>
</html>
```

## Displaying Content


To verify, open a web browser and navigate to the application homepage, followed by `welcome/hello`. The 'Hello World' message should be displayed on the screen.



    ![browser screenshot](images/3/_hello_wHCMx.png)
    
*Screenshot taken from the URL, <base-url>welcome/hello*


