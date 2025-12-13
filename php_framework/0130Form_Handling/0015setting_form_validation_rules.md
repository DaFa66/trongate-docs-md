# Setting Form Validation Rules


Form validation is a crucial aspect of web development, ensuring that user-submitted data meets the required criteria before being processed or stored. Proper validation not only improves user experience by providing immediate feedback but also protects your application from common security threats such as SQL injection, cross-site scripting (XSS), and data corruption. The Trongate PHP framework provides a robust and flexible validation system that simplifies the process of validating form inputs.

## Overview of Trongate's Validation System


Trongate's validation system is designed to be intuitive and easy to use. It allows developers to define validation rules for form fields, automatically handle error messages, and ensure that only valid data is processed. The validation process is managed by the [Validation class](documentation-ref/list_refs/class_reference/the-validation-class), which provides methods for setting rules, running validation checks, and handling errors.

### Key Features of Trongate's Validation System


- **Flexible Rule Definition**: You can define validation rules for each form field, including required fields, minimum and maximum lengths, numeric values, email validation, and more. For example, you can easily set rules like `required|min_length[2]|max_length[255]` to ensure a username is between 2 and 255 characters long.
- **Automatic Error Handling**: The system automatically generates and displays error messages for invalid inputs, making it easy to provide feedback to users. Error messages can be displayed either as a block at the top of the form or inline next to each field.
- **CSRF Protection**: Trongate includes built-in CSRF (Cross-Site Request Forgery) protection to secure your forms against malicious attacks. Each form submission is automatically checked for a valid CSRF token, ensuring that the request originated from your application.
- **Custom Validation**: You can create custom validation rules and callbacks to handle specific validation requirements. For example, you can enforce rules like "The last name cannot be 'Rambo'" by defining a custom validation method.

## Implementing Form Validation in Trongate


Let's walk through the process of implementing form validation in a Trongate application.

### Step 1: Define Validation Rules


In your controller (e.g., `Tasks.php`), you can define validation rules for each form field using the `set_rules` method. This method takes three parameters:


1. **Field Name**: The name of the form field.
2. **Field Label**: The label used in error messages.
3. **Validation Rules**: A string or array of rules to apply to the field.


For example, in the `submit` method of the `Tasks` controller, the following rules are defined for the `task_title` and `task_description` fields:

```php
$this->validation->set_rules('task_title', 'Task Title', 'required|min_length[2]|max_length[255]');
$this->validation->set_rules('task_description', 'Task Description', 'required|min_length[2]');
```


These rules ensure that:


- The `task_title` field is required, has a minimum length of 2 characters, and a maximum length of 255 characters.
- The `task_description` field is required and has a minimum length of 2 characters.

### Step 2: Run the Validation


After defining the validation rules, you can run the validation checks using the `run` method. This method returns `true` if all validation rules pass, or `false` if any validation errors occur.

```php
$result = $this->validation->run();

if ($result === true) {
  // Validation passed, process the form data
} else {
  // Validation failed, redisplay the form with error messages
  $this->create();
}
```


If validation fails, the form is redisplayed with error messages, allowing the user to correct their inputs.


---

## An Alternative Syntax for Setting Form Validation Rules


While the pipe symbol syntax, as demonstrated earlier, is efficient and concise, it can become unwieldy when dealing with forms that contain multiple fields and complex validation rules. To address this, the Trongate framework offers an alternative syntax for setting form validation rules: **Array-Based Rule Setting**. This approach provides a more structured, readable, and maintainable way to define validation rules for your forms.

### How It Works


In the Array-Based approach, instead of chaining validation rules using the pipe symbol `|`, you define each rule as part of an associative array. In this syntax, the keys represent the form field names, and each field is assigned an array of validation rules. This provides better organisation and flexibility, especially for forms with many fields and complex requirements. Here's an example:

```php
$username_rules = array(
    'required' => true,
    'min_length' => 2,
    'max_length' => 255
);
$validation_rules['username'] = $username_rules;
```


Now, let's compare the two approaches for setting validation rules:


**Using the Pipe Symbol to Chain Validation Rules:**

```php
$this->validation->set_rules('username', 'Username', 'required|min_length[2]|max_length[255]');
$this->validation->set_rules('first_name', 'First Name', 'required|min_length[2]|max_length[255]');
$this->validation->set_rules('last_name', 'Last Name', 'required|min_length[2]|max_length[255]');
$this->validation->set_rules('email_address', 'Email Address', 'required|valid_email');
```


**Using Array-Based Syntax to Define Validation Rules:**

```php
// Define validation rules for username
$username_rules = array(
    'required' => true,
    'min_length' => 2,
    'max_length' => 255
);
$validation_rules['username'] = $username_rules;

// Define validation rules for first name
$first_name_rules = array(
    'required' => true,
    'min_length' => 2,
    'max_length' => 255
);
$validation_rules['first_name'] = $first_name_rules;

// Define validation rules for last name
$last_name_rules = array(
    'required' => true,
    'min_length' => 2,
    'max_length' => 255
);
$validation_rules['last_name'] = $last_name_rules;

// Define validation rules for email address
$email_address_rules = array(
    'required' => true,
    'valid_email' => true
);
$validation_rules['email_address'] = $email_address_rules;

// Execute validation
$result = $this->validation->run($validation_rules);
```


While the array-based syntax requires more lines of code, it offers a more organised structure and takes up less horizontal space compared to the pipe symbol approach. Ultimately, the choice between these two methods depends on your project's needs and your preferred coding style.

> [!NOTE]
> **Just To Let You Know...**
>
> When performing form validation, the framework ensures consistency between the validation process and subsequent data processing by automatically applying data cleaning rules through the `post()` function.
> 
> 
> Consider the following:
> 
> ```php
> $this->validation->set_rules('username', 'Username', 'required');
> ```
> 
> 
> With the above code, the validation system will evaluate the result of:
> 
> ```php
> $username = post('username', true);
> ```
> 
> 
> For this reason, to maintain consistency and prevent validation bypasses, values should be retrieved *after* validation using the same approach:
> 
> ```php
> // Example of correct post-validation data retrieval
> private function get_data_from_post() {
>     $data['username'] = post('username', true);
>     $data['email'] = post('email', true);
>     return $data;
> }
> 
> // Example usage in a submit method
> public function submit() {
>     $this->validation->set_rules('username', 'Username', 'required|min_length[2]');
>     $this->validation->set_rules('email', 'Email', 'required|valid_email');
>     
>     if ($this->validation->run() === true) {
>         $data = $this->get_data_from_post();  // Correctly retrieves cleaned data
>         // Process $data...
>     }
> }
> ```
> 
> 
> In situations where it's not acceptable to fetch posted values - after validation - using `post($str, true)`, it's advisable to consider using  [custom validation](0016custom_form_validation_rules.md). This ensures that your validation rules can properly account for any special data handling requirements.


## Key Points Regarding Setting Validation Rules


- Each form field is assigned its own set of validation rules within a sub-array.
- Validation rules are defined as key-value pairs within each field's sub-array.
- The main `$validation_rules` array uses field names as keys.


All of the validation rules that have been used in this page are built into the framework.  In other words, the inner workings of the various validation rules have been written into the Trongate framework.  In the next section, we'll explore how to set your own custom form validation rules.

