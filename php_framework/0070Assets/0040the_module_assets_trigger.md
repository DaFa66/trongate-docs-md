# The Module Assets Trigger


In the example from the previous page, a JavaScript file was successfully served from deep within our 'modules' directory. The target JavaScript file was loaded by setting a source ('src') value of:


`welcome_module/js/ahoy.js`


Under normal circumstances, such a short and concise file destination would produce file loading errors. However, the JavaScript file could be loaded without issue by invoking Trongate's **Module Assets Trigger**.

```php
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

## Understanding the Module Assets Trigger


The *Module Assets Trigger* serves as a specific string included in website URLs or file paths. When encountered, the File Asset Manager initiates a process to locate the requested asset within a module's *assets* directory. Assuming the file exists, the File Asset Manager handles the necessary file retrieval and response headers, facilitating modular development.


By default, the Trongate framework's Module Assets Trigger is defined as the string '_module'. Any path containing this trigger prompts Trongate to identify and fetch files from the respective module's assets directory.

> [!CAUTION]
> If *any* part of a URL or file path contains the Module Assets Trigger, Trongate's File Asset Manager will be invoked and the framework will attempt to serve files from within the application's 'modules' directory. This can lead to confusion and unwanted 404 errors. Therefore, it's advisable to exercise caution when naming modules and files. In particular, steps should be taken to ensure that modules and files do **not** contain the Module Assets Trigger within their assigned names.


## Configuration and Usage


The Module Assets Trigger is configured within the `config.php` file using the following line:

```php
define("MODULE_ASSETS_TRIGGER", "_module");
```


This configuration instructs Trongate to detect and interpret URLs or file paths containing '_module' to fetch assets from the corresponding module's assets directory. For example, to reference a file within the 'cars' module, the path should begin with:

```php
cars_module/
```


This indicates that the asset is located within the 'assets' subdirectory of the 'cars' module.

## Customization Options


If customization of the Module Assets Trigger is necessary to suit specific preferences or naming conventions, simply modify the value assigned to `MODULE_ASSETS_TRIGGER` in the `config.php` file.

> [!TIP]
> **Best Practices**
>
> When developing applications that interact with user input, consider implementing validation rules to prevent inadvertent triggering of the File Asset Manager. For instance, ensure that user-generated URLs or paths do not inadvertently contain the Module Assets Trigger phrase.


