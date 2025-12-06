# Dynamic Module Loading


Trongate’s dynamic module loading system is a standout feature of the framework, giving developers the ability to build scalable, modular applications with ease. With Trongate's module loading system, developers can use self-contained modules on demand, eliminating the need for excessive dependencies or cluttered codebases. Whether you're handling security, file uploads, or user management, modules integrate seamlessly, making it easier than ever to extend your application’s functionality. This page will walk you through how modules are dynamically loaded in Trongate.

## How Dynamic Module Loading Works


In Trongate, modules are self-contained components that encapsulate specific functionality, such as security, file uploads, or user management. These modules can be loaded dynamically into your controllers, making it easy to extend the functionality of your application without modifying the core framework.

### Step-by-Step Process


1. **Loading a Module:**
To load a module, simply call the module() method in your controller and pass the name of the module as a parameter. For example:

```php
$this->module('trongate_security');
```


This method delegates the loading process to the [Modules class](documentation-ref/list_refs/class_reference/the-modules-class), which handles the instantiation and attachment of the module to your controller.


2. **Dynamic Property Attachment:**
Once a module is loaded, it is dynamically attached to the [Trongate](documentation-ref/list_refs/class_reference/the-trongate-class) instance as a property. For example, after calling `$this->module('trongate_security');`, the [Trongate Security](documentation-ref/list_refs/pre_installed/trongate-security) module becomes accessible via `$this->trongate_security`.


3. **Using the Module:**
After loading the module, you can immediately use its methods. For example:

```php
$this->trongate_security->_make_sure_allowed();
```


This seamless integration ensures that modules are ready to use as soon as they are loaded, without any additional configuration.




---

## Under the Hood: How Dynamic Module Loading Works


To truly understand the power of Trongate’s dynamic module loading, let’s take a closer look at the underlying mechanisms:

### The Role of the module() Method


The module() method in the [Trongate class](documentation-ref/list_refs/class_reference/the-trongate-class) acts as a bridge between your controller and the [Modules class](documentation-ref/list_refs/class_reference/the-modules-class). When you call `$this->module('trongate_security');`, the following happens:


1. The module() method creates an instance of the [Modules class](documentation-ref/list_refs/class_reference/the-modules-class):
```php
$modules = new Modules;
```


2. It then calls the load() method of the [Modules class](documentation-ref/list_refs/class_reference/the-modules-class), passing the name of the module to be loaded:
```php
$modules->load($target_module);
```



### The Role of the Modules Class


The [Modules class](documentation-ref/list_refs/class_reference/the-modules-class) is responsible for dynamically loading and instantiating modules. Here’s how it works:


1. The load() method constructs the path to the module’s controller file based on the module name:
```php
$target_controller_path = '../modules/' . $target_module . '/controllers/' . ucfirst($target_module) . '.php';
```


2. If the controller file exists, it is included, and the module’s controller class is instantiated:
```php
$this->modules[$target_module] = new $target_module($target_module);
```


3. The instantiated module is stored in the `$modules` array within the [Modules class](documentation-ref/list_refs/class_reference/the-modules-class), ensuring that it can be reused if needed. This caching mechanism prevents redundant instantiations of the same module during a single request, improving performance.

### The Role of the Dynamic_properties Trait

> [!NOTE]
> **Just To Let You Know...**
>
> Trongate's dynamic module loading system is made possible by the `Dynamic_properties` trait, which allows properties to be added to the `Trongate` instance at runtime. This is achieved using PHP's magic methods (`__get()` and `__set()`), enabling safe access and manipulation of dynamically added properties.
> 
> 
> This is called at the top of the main Trongate class with the following line of code:
> 
> ```php
> use Dynamic_properties;
> ```
> 
> 
> The remainder of this page contains information about how Trongate's dynamic module loading system works under the hood. However, it should be stressed that there's no requirement to understand *how* the internals of Trongate work to use the framework effectively.



The `Dynamic_properties` trait enables the [Trongate class](documentation-ref/list_refs/class_reference/the-trongate-class) to handle properties that are not explicitly defined. Here’s how it works:


1. When a module is loaded, the `Dynamic_properties` trait allows the module to be dynamically attached to the [Trongate](documentation-ref/list_refs/class_reference/the-trongate-class) instance as a property. For example:
```php
$this->trongate_security = new Trongate_Security('trongate_security');
```


2. This dynamic property attachment ensures that the module is accessible throughout the `Trongate` instance, allowing you to call its methods directly. For example:
```php
$this->trongate_security->_make_sure_allowed();
```




The `Dynamic_properties` trait is essential for enabling this flexibility, as it allows properties like `$this->trongate_security` to be added dynamically without requiring explicit declarations in the [Trongate class](documentation-ref/list_refs/class_reference/the-trongate-class).


---

## Benefits of Trongate’s Module Loading System


Trongate’s dynamic module loading system offers several advantages that make it a powerful tool for developers:


- **Modular Architecture:** Trongate’s modular design promotes separation of concerns, making your codebase cleaner and easier to maintain.
- **Ease of Use:** With just a single line of code (`$this->module('module_name');`), you can load and use any module in your application.
- **Flexibility and Extensibility:** The ability to dynamically attach modules ensures that Trongate can adapt to the needs of your project.
- **Lightweight and Efficient:** Trongate’s module loading mechanism is designed to be lightweight and efficient, ensuring that your application remains performant.
- **Developer-Friendly:** The intuitive design of Trongate’s module loading system makes it accessible to developers of all skill levels.

## In Summary


Trongate’s dynamic module loading system is a cornerstone of its architecture, providing developers with a powerful and flexible way to build modular applications. By leveraging the internal `Dynamic_properties` trait, Trongate ensures that modules can be seamlessly integrated into your controllers, enhancing both functionality and maintainability.


Whether you’re building a simple website or a large-scale, complex web application, Trongate’s module loading system empowers you to create clean, modular, and extensible code with minimal effort.

> [!NOTE]
> **Just To Let You Know...**
>
> For more information on how to work with Trongate's dynamic module loading system please refer to the chapter, [Modules Calling Modules](documentation/display/php_framework/modules-calling-modules).


