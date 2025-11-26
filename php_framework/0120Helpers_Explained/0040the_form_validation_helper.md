# The Form Validation Helper


Trongate's validation helper uses server side validation to assist developers in validating submitted form values.


All form validation procedures these following three steps:


- Submitted form values are passed through some validation test.
- The results from the validation tests are assigned a boolean value of **true** (if the submitted form *passes* validation tests) or **false** (if there was at least one form validation error).
- The user is then presented with either a 'success' message or some validation errors, based on the results of the validation tests.

> [!WARNING]
> A complete walk-through of how form validation works is available in the 'Form Handling' chapter of these docs.


## How To Set Form Validation Rules


Form validation rules can be set by calling upon the validation helper and then invoking Trongate's inbuilt 'set_rules' method. This should be used on a line-by-line basis, whereby each form field that requires validation is processed via a line of code which takes the form:

```php
$this->validation->set_rules("name", "label", "rule");
```

## How To Pipe Multiple Rules Together


Trongate lets you apply multiple validation rules to a submitted value by joining rules together by use of the pipe symbol. For example:

```php
$this->validation->set_rules("name", "label", "rule1|rule2|rule3");
```

## Running Form Validation Tests


The form validation tests that you have created can be applied by calling the validation helper's **run()** method. Calling run() will produce *true* if the values passed validation tests and *false* if there was at least one form validation error.

```php
$result = $this->validation->run();
```

## Displaying Validation Errors


If there are validation errors, they can be displayed by calling Trongate's in-built validation_errors() method from within a view file. For example:

```php
<?= validation_errors() ?>
```

## Formatting Validation Errors


By default, each validation error is displayed as a paragraph with red text. However, you can modify the appearance of validation errors by adding opening and closing tags inside your validation_errors() declaration. For example:

```php
formatted-errors
```

## Validation Rules Reference


form-validation-table

