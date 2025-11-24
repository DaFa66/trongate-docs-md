# run_validation_test()


private function run_validation_test(array $validation_data, $rules = null): void

## Description

Executes a specific validation test based on the provided validation data and rules. This method is part of Trongate's robust Validation class.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $validation_data | array | An array containing validation data, including the 'test_to_run' key. |
| $rules | mixed\|null | (optional) Additional rules for validation, used in specific cases like file validation. Default is null. |

## Return Value


| Type | Description |
| ---|---|
| void | This function does not return a value. It updates the internal state of the validation object. |

## Example #1


The code sample below demonstrates how to set up validation rules for a 'username' field in a Trongate controller:

```php
public function submit(): void {
      $this->validation->set_rules('username', 'Username', 'required|min_length[2]|max_length[255]');
      
      $result = $this->validation->run();

      if ($result) {
          echo 'Form submission successful!';
      } else {
          $this->create();
      }
  }
```

## Example #2


This example shows how to use array-based validation for multiple fields:

```php
public function submit(): void {
      $validation_rules['username'] = [
          'required' => true,
          'min_length' => 2,
          'max_length' => 255
      ];
      $validation_rules['email_address'] = [
          'required' => true,
          'valid_email' => true
      ];

      $result = $this->validation->run($validation_rules);

      if ($result) {
          echo 'Form submission successful!';
      } else {
          $this->create();
      }
  }
```

## Notes


- This is a private method used internally by Trongate's Validation class.
- The method supports various validation tests including: required, numeric, integer, decimal, valid_email, validate_file, valid_datepicker, valid_datetimepicker, and valid_time.
- Custom validation rules can be created using callback functions, prefixed with 'callback_' in the set_rules() method.
- The Validation class automatically includes CSRF protection checks when the run() method is called.
- To display validation errors, you can use the validation_errors() function after run() returns false.
