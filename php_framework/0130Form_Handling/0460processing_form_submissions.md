# Processing Form Submissions


In Trongate, after form validation is complete, the next crucial step is processing the submitted data. This section covers the implementation patterns for handling validated form data.

## The Data Processing Workflow


A typical form processing workflow in Trongate follows this pattern:

```php
public function submit(): void {
   $this->module('trongate_security');
   $this->trongate_security->_make_sure_allowed();

   $submit = post('submit', true);
   if ($submit === 'Submit') {
       // Validation occurs here (covered in previous section)
       if ($this->validation->run() === true) {
           $this->process_valid_submission();
       } else {
           $this->create(); // Return to form with errors
       }
   }
}
```

## Processing Valid Submissions


When handling validated form data, you'll typically need to:


1. Collect the submitted data
2. Determine the operation type (insert or update)
3. Perform the database operation
4. Provide user feedback
5. Direct the user to the next appropriate page


Here's a real-world example that demonstrates this workflow:

```php
private function process_valid_submission(): void {
   $update_id = segment(3, 'int');
   $data = $this->get_data_from_post();
   
   if ($update_id > 0) {
       $this->model->update($update_id, $data, 'employees');
       $flash_msg = 'Employee record successfully updated';
   } else {
       $update_id = $this->model->insert($data, 'employees');
       $flash_msg = 'New employee record successfully created';
   }

   set_flashdata($flash_msg);
   redirect('employees/show/' . $update_id);
}
```

### Data Collection Strategies


The `get_data_from_post()` method is crucial for organizing form data. Here's an example that includes data transformation:

```php
private function get_data_from_post(): array {
   // Basic field collection
   $data['first_name'] = post('first_name', true);
   $data['last_name'] = post('last_name', true);
   
   // Transform checkbox value to boolean
   $data['is_active'] = (post('is_active', true) === '1') ? 1 : 0;
   
   // Format date for database
   $hire_date = post('hire_date', true);
   $data['hire_date'] = date('Y-m-d', strtotime($hire_date));
   
   return $data;
}
```

> [!NOTE]
> **Just To Let You Know...**
>
> When performing form validation, the framework ensures that the data being validated matches the data that will be processed. This is achieved through the integration of the `post()` function in the validation process.
> 
> 
> For example, when the following validation rule is declared:
> 
> ```php
> $this->validation->set_rules('username', 'Username', 'required');
> ```
> 
> 
> The validation system will internally evaluate:
> 
> ```php
> $value = post('username', true);
> ```
> 
> 
> The `post()` function, when called with a second argument of `true`, performs two cleaning operations:
> 
> 
> - Removes whitespace from the beginning and end of strings
> - Normalizes internal spacing (multiple spaces become single spaces)
> 
> 
> Therefore, to maintain consistency between validation and data processing, values should be retrieved *after* validation using `post($str, true)`. In situations where this cleaning behavior is not acceptable, it's advisable to consider using custom validation.


