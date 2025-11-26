# What Are Parent And Child Modules?

> [!WARNING]
> Previously, child modules required additional code in order to work. Specifically, they required a constructor and destructor. You may have even seen tutorials going over this. However, the additional code for child modules is no longer a requirement. Ordinary modules can work inside ordinary modules.



The Trongate framework gives developers the ability to have modules contained *within* modules. When a module contains one or more modules, the parent module is referred to as being a ***parent module***. In Trongate, child modules (i.e., modules that are contained within parent modules) are called ***child modules***.


There's no command line required and definitely no need for any Packagist, Composer or vendor/autoload!


Imagine being able to drop just *one* directory into your app and immediately having:


- A complete invoicing system
- A complete online shop
- A complete discussion forum
- Or, any other advanced feature that you care to imagine!


**Trongate makes this possible.**


All you have to do - to take advantage of parent modules and child modules - is add a module inside an existing module and also be aware of a few rules that will assist you in calling your child modules.

