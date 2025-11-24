# anchor()


function anchor(string $url, ?string $text = null, array $attributes = []): string

## Description

Generates an anchor (<a>) tag with optional attributes and partial XSS protection.


This function creates an anchor tag pointing to a specified URL. If the `$text` parameter is omitted, the URL itself is used as the link text.


**Important:** The `$text` parameter is NOT escaped, allowing HTML content to be rendered as-is, while the URL and attributes are automatically escaped to prevent XSS attacks.
## Parameters


| Name | Type | Description |
| ---|---|---|
| $url | string | The URL to link to. This parameter is required and will be automatically escaped. |
| $text | string\|null | The text content of the link (optional). If not provided, the URL itself is used. **Note:** This parameter is NOT escaped. |
| $attributes | array | An optional array of key-value pairs for additional attributes. These values will be automatically escaped. |

## Return Value


| Type | Description |
| ---|---|
| string | The complete HTML anchor tag as a string. |

## Example Usage

```
// Basic usage with just URL
echo anchor('contact');
// Output: <a href="contact">contact</a>

// Basic usage with URL and text
echo anchor('contact', 'Get In Touch');
// Output: <a href="contact">Get In Touch</a>

// With attributes
echo anchor('logout', 'Sign Out', ['class' => 'btn btn-danger', 'rel' => 'nofollow']);
// Output: <a href="logout" class="btn btn-danger" rel="nofollow">Sign Out</a>

// External link with target and rel attributes
echo anchor('https://github.com/trongate', 'View Repo', ['target' => '_blank', 'rel' => 'noopener noreferrer']);
// Output: <a href="https://github.com/trongate" target="_blank" rel="noopener noreferrer">View Repo</a>

// Using HTML within text parameter (intentionally not escaped)
echo anchor('contact', '<i class="fa fa-envelope"></i> Contact Us');
// Output: <a href="contact"><i class="fa fa-envelope"></i> Contact Us</a>
```
## Security Considerations


**Important:** The `$text` parameter is not automatically escaped. If displaying user-generated content, use the `out()` function to prevent XSS attacks.


**Unsafe Example (Vulnerable to XSS):**

```
echo anchor('profile', $user_name); 
// Output (potentially unsafe): <a href="profile"><script>alert('XSS')</script></a>
```


**Safe Example (Escaped Output):**

```
echo anchor('profile', out($user_name)); 
// Output: <a href="profile">John Doe</a>
```


**Note:** The `$url` and `$attributes` parameters are automatically escaped for security.
