# Redirect on Success


In certain situations, you may wish to redirect users to a different URL after receiving a success status code (200-299) from an API endpoint. The `mx-redirect-on-success` attribute is specifically designed for this purpose.

## Usage


To use `mx-redirect-on-success`, add it to any element that triggers an HTTP request (such as forms or buttons) and set its value to "true". The redirect URL should be returned as plain text in the response body from the server.

> [!WARNING]
> The redirect happens immediately upon receiving a successful response from the target API endpoint. Because of this, `mx-redirect-on-success` should **not** be combined with animation attributes or other success handlers since they won't have time to execute.


### Basic Example:


The code sample below would render a form button that - when clicked - invokes an HTTP post request.  If the server responds with an HTTP status code in the 'success' range (for example, **200**), the user will be immediately redirected to the URL that is specified in the response body.

```vf
<?php
$btn_attr = [
  'mx-post' => 'members/goto_dashboard',
  'mx-token' => $trongate_token,
  'mx-redirect-on-success' => 'true'
];
echo form_button('action_btn', 'View Dashboard', $btn_attr);
?>
```


Here's an alternative syntax for developers who prefer to work with pure HTML:

```vf
<button mx-post="members/goto_dashboard" 
        mx-token="<?= $trongate_token ?>"
        mx-redirect-on-success="true">View Dashboard</button>
```

> [!NOTE]
> **Just To Let You Know...**
>
> The code sample above assumes that a `$trongate_token` value has been passed into the view file from a controller file.


## Server-Side Implementation


For the redirect to work correctly, your API endpoint must:


1. Return a success status code (200-299).
2. Return only the redirect URL as plain text in the response body.

### Example Controller Code:

```php
public function goto_dashboard() {
  $this->module('trongate_tokens');
  $trongate_token = $this->trongate_tokens->_attempt_get_valid_token();

  if ($trongate_token !== false) {
    http_response_code(200);
    echo 'dashboard'; // Will redirect to yoursite.com/dashboard
    die();
  }
  
  http_response_code(401);
  echo 'Invalid username or password.';
}
```

## Common Use Cases

### 1. Login Form

```vf
<?php
$form_attr = [
    'mx-post' => 'members/submit_login',
    'mx-redirect-on-success' => 'true'
];
echo form_open('#', $form_attr);

$username_attr['placeholder'] = 'Enter username here...';
echo form_input('username', '', $username_attr);

$password_attr['placeholder'] = 'Enter password here...';
echo form_password('password', '', $password_attr);

echo form_submit('submit_btn', 'Login');
echo form_close();
?>
```

### 2. Multi-Step Process

```vf
<?php
$btn_attr = [
  'mx-post' => 'payment/process',
  'mx-target' => '#payment-status',
  'mx-redirect-on-success' => 'true'
];
echo form_button('payment_btn', 'Complete Payment', $btn_attr);
?>
```

> [!WARNING]
> **The following considerations should be taken into account:**
> 
> 
> - The response body must contain only the URL - any additional content will prevent the redirect.
> - The redirect occurs immediately upon receiving a successful response.
> - Cannot be used with animation attributes since the redirect is immediate.


## URL Handling


The redirect URL can be specified in several ways:


- Relative to your site root (e.g., 'dashboard').
- Starting with a forward slash (e.g., '/dashboard').
- As an absolute URL (e.g., 'https://example.com/dashboard').

> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** For relative URLs to work correctly, your page should include a `<base>` tag in the head section. For example:
> 
> ```html
> <base href="<?= BASE_URL ?>">
> ```
> 
> 
> Without a base tag, relative URLs might not resolve to the correct location.


> [!TIP]
> **Best Practices**
>
> For comprehensive navigation flows, consider using both `mx-redirect-on-success` and 
>   `mx-redirect-on-error` together to handle both successful and failed scenarios.


## Summary


The `mx-redirect-on-success` attribute is a handy way to redirect users after a successful form submission.  However, there are a wide variety of other scenarios where it could be useful.


By simply specifying a URL, you can guide users seamlessly to the next step in their journey - no extra JavaScript required! Whether you're using pure HTML or Trongate's helper functions, this attribute makes building smooth, user-friendly experiences a breeze.

