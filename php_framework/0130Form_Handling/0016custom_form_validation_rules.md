# Custom Form Validation Rules


In certain scenarios, you may need to implement form validation checks that go beyond the built-in rules provided by Trongate's [Validation class](../../reference/class_reference/The_Validation_Class). In such cases, **custom form validation callbacks** become invaluable.

## General Concept


When using Trongate's [Validation class](../../reference/class_reference/The_Validation_Class) to apply form validation checks, the set_rules method plays a crucial role in defining the validation rules for specific form fields. For instance, the following code ensures that both the 'first_name' and 'last_name' fields must:


- Not be empty
- Be at least 2 characters long
- Be no more than 255 characters long

```php
$this->validation->set_rules('first_name', 'first name', 'required|min_length[2]|max_length[255]');
$this->validation->set_rules('last_name', 'last name', 'required|min_length[2]|max_length[255]');
```

## Adding Custom Validation Checks


To implement validation rules *not* covered by Trongate's default tests, you can create custom validation callbacks. For example, let's say you want to enforce the rule: "**The last name cannot be 'Rambo'**". To do this, follow these steps:


1. Declare the custom validation check.
2. Create a method to define the behavior of the custom validation check.

## Declaring a Custom Validation Check


To declare a custom validation rule, prepend the rule name with '**callback_**', followed by the name of the method that will handle the validation logic. For example, if you have a method called **`check_last_name()`** for this custom validation, you would append it to the `set_rules` declaration for 'last_name' field, like so:

```php
|callback_check_last_name
```


This means the block of code for applying form validation rules would now look like this:

```php
$this->validation->set_rules('first_name', 'first name', 'required|min_length[2]|max_length[255]');
$this->validation->set_rules('last_name', 'last name', 'required|min_length[2]|max_length[255]|callback_check_last_name');
```

> [!TIP]
> **Best Practices**
>
> While it's not required, it's recommended to adhere to Trongate's [Underscore Naming Convention](../0030Basic_Concepts/0015the_underscore_naming_convention.md) whenever creating custom methods.


## Creating a Custom Validation Method


Custom validation methods automatically receive the posted form field value as an argument and should return either a boolean **`true`** (indicating validation success) or an error message (as a string). The following demonstrates the basic structure of a typical custom validation callback method:

```php
function check_last_name($last_name) {
    // Perform custom validation
}
```

> [!NOTE]
> **Just To Let You Know...**
>
> Custom form validation callback methods should **only** return one of the following two things:
> 
> 
> 1. A **string** with a form validation error message, if the submitted value *fails* the validation test.
> 2. A boolean of **true**, if the submitted value *passes* the validation test.
> 
> 
> The behaviour of custom form validation callbacks may be described more fully by adding [access modifiers](https://www.w3schools.com/php/php_oop_access_modifiers.asp), doc blocks, type hinting and return types, like so:
> 
> ```php
> /**
>  * Validates a string input.
>  *
>  * This custom validation method performs a check on the provided string value.
>  * If the value fails validation, an error message is returned. If the value passes,
>  * the method returns true.
>  *
>  * @param string $str The string to validate.
>  * @return string|true Returns an error message if the string fails validation, otherwise returns true.
>  */
> public function check_last_name(string $str): string|true {
>     // Perform custom validation
> }
> ```



To implement the custom rule where the last name cannot be "Rambo", the method would look like this:

```php
function check_last_name($last_name) {
    if ($last_name === 'Rambo') {
        return 'We don\'t want guys like you in this town.';
    } else {
        return true;
    }
}
```


If the submitted `last_name` fails the custom validation check, the following error message will be returned:


**We don't want guys like you in this town.**


On the other hand, if the submitted `last_name` passes the custom validation, the method will return **`true`**, and no error message will be generated.

> [!TIP]
> **Best Practices**
>
> For enhanced code clarity and functionality, consider using doc blocks, access modifiers, type hints, and return types in your validation callback methods. Though optional, these practices improve code readability and maintainability. For example:
> 
> ```php
> /**
>  * Validates that the last name is not 'Rambo'.
>  *
>  * @param string $last_name The last name to validate.
>  * @return string|true Returns an error message if the last name is 'Rambo', otherwise returns true.
>  */
> public function check_last_name(string $last_name): string|true {
>     if ($last_name === 'Rambo') {
>         return 'We don\'t want guys like you in this town.';
>     } else {
>         return true;
>     }
> }
> ```
> 
> 
> To learn more about docblocks, type hinting, and return types check out this [YouTube tutorial](https://www.youtube.com/watch?v=R76Um_oIZNY).
> 
> 
> By the way, there appears to be some ambiguity, in the PHP community, about how to write 'doc blocks'.  Should it be two words, one word or something to do with camelCase?  If you know the answer, please [let us know](https://trongate.io/contactus)!



In the next section, we will explore how display form validation errors.

