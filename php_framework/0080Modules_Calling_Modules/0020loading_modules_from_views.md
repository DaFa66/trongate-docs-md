# Loading Modules From Views


Within the Trongate framework, it is possible to load another module from within a view file. This capability provides additional flexibility and allows for dynamic content generation within views.


To load a module from a view file, use the following syntax:

```vf
<?= Modules::run("module_name/method_name") ?>
```

## Why Use This Approach?


There are various scenarios where loading a module from within a view file can be advantageous. For instance, consider the need to include a 'Stripe' payment button on a webpage. When users click the 'Buy Now' button, a pop-up might appear, prompting the user to enter payment details. The implementation of such a feature can be complex and is best handled by a dedicated 'stripe' module.


Having a separate 'stripe' module that manages everything related to Stripe payments, including rendering the pop-up payment modal, allows you to maintain clean and organized code. This module can be easily called from any view file with a single line of code, as shown below:

```vf
<?= Modules::run("stripe/render_payment_button") ?>
```

## Passing Arguments


When calling modules from view files, arguments can be passed to the methods. This is done by separating the arguments with commas. Below is an example where a variable called `$name` is passed as an argument:

```vf
<?= Modules::run("welcome/greeting", $name) ?>
```

