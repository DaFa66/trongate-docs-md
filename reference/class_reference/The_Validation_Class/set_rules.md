# set_rules()


public function set_rules(string $key, string $label, string|array $rules): void

## Description

Set rules for form field validation.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| $key | string | The form field name. |
| $label | string | The form field label. |
| $rules | string\|array | The validation rules for the field. |

## Return Value

This method does not return any value (void).
## Example Usage

```php
$this->validation->set_rules('username', 'Username', 'required|min_length[5]|max_length[20]');
$this->validation->set_rules('email', 'Email', ['required', 'valid_email']);
```
