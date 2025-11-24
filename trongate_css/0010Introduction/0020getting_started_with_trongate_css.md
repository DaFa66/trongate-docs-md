# Getting Started


Trongate CSS is contained within a single CSS file named '**trongate.css**'. This file is located in:

```
public/ 
  css/ 
    trongate.css
```

## Basic Usage


Trongate CSS comes with every new installation of Trongate. Getting up and running with Trongate CSS is easy!


Let's assume your starting point is a webpage (within a Trongate application) containing the following source code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
   <h1>Hello, Trongate CSS!</h1>
</body>
</html>
```


**Step 1: ** Add a `<base>` element to the `<head>` section of your webpage with the 'href' attribute set to your application's base URL:

```html
<base href="<?= BASE_URL ?>">
```

> [!NOTE]
> **Just To Let You Know...**
>
> The `BASE_URL` constant is defined inside the file '**config.php**'. This constant should be set to a website address pointing to the homepage of your web application.
> 
> 
> The **config.php** file is located in:
> 
> ```
> public/ 
>     config/ 
>       config.php
> ```



**Step 2: ** Load the Trongate CSS stylesheet onto your webpage by adding the following new line of code to the `<head>` section:

```html
<link rel="stylesheet" href="css/trongate.css">
```

> [!NOTE]
> **Just To Let You Know...**
>
> After completing the steps above, Trongate CSS will automatically style your HTML elements without requiring additional classes or configuration.


## Boilerplate HTML


The HTML code below demonstrates a basic, reusable template containing the essential structure and elements needed to start working with Trongate CSS:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <base href="<?= BASE_URL ?>">
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="css/trongate.css">
  <title>Document</title>
</head>
<body>
   <h1>Hello, Trongate CSS!</h1>
</body>
</html>
```

