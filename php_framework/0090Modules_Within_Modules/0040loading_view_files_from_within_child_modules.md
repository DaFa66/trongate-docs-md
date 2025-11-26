# Loading View Files From Within Child Modules


There may be situations where you'd like to load a view file from within a child module - specifically, by calling (invoking) the view from within a child module's controller. As a reminder, Trongate offers two methodologies for loading of view files. They are:

To load a view file and have it display inside a template.To load a view file on its own - without loading a template.
**LOADING VIEWS WITHIN TEMPLATES**


Normal Trongate usage usually has view files displayed by defining a 'view_file' property, loading a template and passing the 'view_file'. property into the template request as part of a data array. To achieve this from within a child module, the following two steps are required:


**STEP 1**: Declare a 'view_module' property, as part of a $data array, within your child module controller file. Make sure your view module contains the name of the parent (super) module then a forward slash followed by the name of the sub (child) module.


**STEP 2**: Declare a 'view_file' property, as is normal, within your controller file.


**EXAMPLE #1**


Let's assume you have a super (parent) module called 'forums' and a sub (child) module called 'forum_threads'. Below is an example of syntax that could be used to load a view file from the 'forum_threads' controller.

```php
function create() {
  $data["view_module"] = "forums/forum_threads";
  $data["view_file"] = "create";
  $this->template("members_area", $data);
}
```

  
> [!WARNING]
> The code sample above would be a method contained within a 'forum_threads' controller file. The URL for invoking the method above would be the BASE_URL followed by forums-forum_threads/create.



**LOADING VIEWS *****WITHOUT***** LOADING TEMPLATES**


The example above show how to load a view file whilst loading a template. However, there may be instances where you'd like to load a view file *without* loading a template. Trongate's default blue page (with the headline "It Totally Works") is an example of scenario where a view file is being called without loading a template.


To achieve this from a child module, the following three steps should be followed:


**STEP 1**: At the top of your controller file (within your child module), declare a parent and child module inside a constructor method. The parent module should be the name of the module that contains your child module. The child module should be the name of the module from where you are calling your view file.


**STEP 2**: At the bottom of your controller file (within your child module), use a destructor method to reset the parent and child modules.


**STEP 3**: Load your view file, from within a method inside your child module, as normal.


**  
EXAMPLE #2  
**  
Let's assume you have a super (parent) module called 'paypal' and a sub (child) module called 'shopping_basket'. We'll further assume that our goal is to invoke a method called '_draw_basket()'. The purpose of the _draw_basket() method is to display a view file. Below is an example of syntax that could be used to load a view file from the 'shopping_basket' controller.

```php
<?php
class Shopping_basket extends Trongate {

  function __construct() {
    parent::__construct();
    $this->parent_module = "paypal";
    $this->child_module = "shopping_basket";
  }

  function _draw_basket($data) {
    $this->view("basket", $data);
  }

  function __destruct() {
    $this->parent_module = "";
    $this->child_module = "";
  }

}
```

> [!WARNING]
> The parent::construct(); declaration - within the constructor - is required if you intend on making database queries from within your child module.


