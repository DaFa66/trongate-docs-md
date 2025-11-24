# Accessing Child Modules From Other Modules

## From Controllers


To call (invoke) a child module from another Trongate module (that's *any* other kind of Trongate module!) we simply continue with our 'parent with a hyphen' policy when we are loading our child modules. **Once the child module class has been successfully loaded, we no longer need to reference the parent module when invoking methods from the child module.**


Below is an example of our display() method - inside 'accessories' - being called from within our 'cars' module:

```php
<?php
class Cars extends Trongate { 

  function index() { 
    $this->module("cars-accessories");
    $this->accessories->display(); 
  }

}
?>
```

## From Views


Child Modules may be called from view files by following our convention of referencing the parent followed by a hyphen, when calling our child modules. For example:

```php
<?= Modules::run("cars-accessories/display") ?>
```

