# post()


function post(string $field_name, bool $clean_up = false): string|int|float|array

## Description

Retrieves a value from POST data, handling both traditional form-encoded data and JSON payloads. It can optionally sanitize and convert the value. The function supports dot notation for accessing nested fields in JSON data, providing a versatile way to handle and clean POST data in your application.
## Parameters


| Parameter | Type | Description |
| ---|---|---|
| `$field_name` | string | The name of the field to retrieve from the POST data. Supports dot notation for accessing nested fields in JSON data. |
| `$clean_up` | bool | Optional. Determines whether to sanitize and convert the retrieved value. Default is `false`. |

## Return Value


| Type | Description |
| ---|---|
| string\|int\|float\|array | The value retrieved from the POST data. If the field is not found, an empty string is returned. If `$clean_up` is `true`, the value is sanitized and potentially converted. For JSON data, it may return an array. |

## Behavior

#### Content Type Handling:


- Automatically detects and handles both form-encoded data and JSON payloads.
- For JSON data, the payload is parsed once and cached for subsequent calls. If parsing fails, an exception is thrown.

#### When $clean_up is false (default):


- Returns the raw value from the POST data if the field exists, or an empty string if it doesn't.
- No sanitization or type conversion is performed.

#### When $clean_up is true:


- **Trimming:** Removes leading and trailing whitespace using `trim()` for string values.
- **Sanitization:** Applies `htmlspecialchars()` to convert special characters to HTML entities in string values, helping prevent Cross-Site Scripting (XSS) attacks.
- **Type Conversion:** If the sanitized value is numeric:
        
- Converts to `int` if the value is a whole number.
- Converts to `float` if the value contains a decimal point.


      
- **Array Handling:** For array values (e.g., from JSON data), applies trimming and sanitization recursively to all string elements.
## Example Usage

```
// Retrieve raw POST data
$username = post('username');

// Retrieve sanitized and potentially converted POST data
$age = post('age', true);

// Example with type conversion
$price = post('price', true);
// If POST data contains '19.99', $price will be float(19.99)
// If POST data contains '20', $price will be int(20)

// Handling JSON data
$jsonData = post('user_data');
// If POST contains JSON like '{"name": "John", "age": 30}',
// $jsonData will be an array(['name' => 'John', 'age' => 30])

// Handling nested JSON data
$street = post('user_data.address.street', true);
// If POST contains JSON like '{"user_data": {"address": {"street": "123 Main St"}}}',
// $street will be "123 Main St" (sanitized)
```
## Security Note

While the `$clean_up` option provides basic sanitization, it's recommended to always validate and sanitize data according to its specific use case. For instance, email addresses, dates, or custom formatted strings may require additional validation or different sanitization methods. When working with JSON data, be cautious of deeply nested structures and potential security implications.
