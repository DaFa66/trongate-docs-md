# Redirect on Error


Sometimes, you may wish to redirect users to a different URL when an API endpoint returns an error status code (400-599). The `mx-redirect-on-error` attribute makes this process straightforward.

## Usage


Simply add `mx-redirect-on-error` to any element that triggers an HTTP request (such as forms or buttons) and set its value to "true". The redirect URL should be returned as plain text in the response body from your server.

> [!WARNING]
> **Warning!**
>
> The redirect happens immediately upon receiving an error response from the target API endpoint. Because of this, `mx-redirect-on-error` should **not** be combined with animation attributes or other error handlers since they won't have time to execute.


### Basic Example:


In the example below, clicking a form button invokes an HTTP POST request.  If the server responds with an HTTP response code that is in the **success** range, the element with an id of 'result' will be updated.  However, if the server responds with an HTTP response code in the **error** range, the user will be redirected to the URL that is specified in the response body.

```vf
<?php
$btn_attr = [
  'mx-post' => 'products/delete/123',
  'mx-target' => '#result',
  'mx-token' => $trongate_token,
  'mx-redirect-on-error' => 'true'
];
echo form_button('delete_btn', 'Delete Product', $btn_attr);
?>

<div id="result"></div>
```


Here's an alternative syntax, for users who prefer to work with pure HTML:

```vf
<button mx-post="products/delete/123"
        mx-target="#result"
        mx-token="<?= $trongate_token ?>"
        mx-redirect-on-error="true">Delete Product</button>

<div id="result"></div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> The code sample above assumes that a `$trongate_token` value has been passed into the view file from a controller file.


## Server-Side Implementation


For the error redirect to work correctly, your API endpoint must:


1. Return an error status code (400-599).
2. Return only the redirect URL as plain text in the response body.

### Example Controller Code:

```php
public function delete_product($product_id) {
  $this->module('trongate_tokens');
  $trongate_token = $this->trongate_tokens->_attempt_get_valid_token();

  if ($trongate_token === false) {
    http_response_code(401);
    echo 'auth/login'; // Will redirect to yoursite.com/auth/login
    die();
  }
  
  if ($this->products->delete($product_id)) {
    http_response_code(200);
    echo 'Product deleted successfully.';
  }
}
```

## Common Use Cases

### 1. Login Form

```vf
<div id="response"></div>

<?php
$form_attr = [
  'mx-post' => 'members/submit_login',
  'mx-target' => '#response',
  'mx-redirect-on-error' => 'true'
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

### 2. Protected Resource Access

```vf
<?php
$btn_attr = [
  'mx-get' => 'products/view/999',
  'mx-target' => '#product-details',
  'mx-redirect-on-error' => 'true'
];
echo form_button('view_product_btn', 'View Product', $btn_attr);
?>

<div id="product-details"></div>
```

> [!WARNING]
> **Warning!**
>
> **A few friendly reminders:**
> 
> 
> - Make sure your response body contains only the URL - any additional content will prevent the redirect from working properly.
> - The redirect happens straight away when an error response is received.
> - You can't use this with error animation attributes since the redirect happens immediately.
> - For handling successful scenarios, consider using `mx-redirect-on-success`.


## URL Handling


You can specify the redirect URL in several ways:


- Relative to your site root (e.g., 'auth/login').
- Starting with a forward slash (e.g., '/auth/login').
- As an absolute URL (e.g., 'https://example.com/auth/login').

> [!NOTE]
> **Just To Let You Know...**
>
> **Tip:** For relative URLs to work properly, make sure your page includes a `<base>` tag in the head section. For example:
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
> For seamless navigation flows, consider using both `mx-redirect-on-error` and 
>   `mx-redirect-on-success` together to handle both successful and failed scenarios.


## Summary


The `mx-redirect-on-error` attribute provides a simple way to handle error scenarios in your web applications. It is especially useful for managing authentication failures, missing resources, or any situation where you need to gracefully redirect users to a different page when things don't go as planned.


Best of all, no extra JavaScript is required — simply return a URL from your API endpoint, and you're good to go! Whether you're building a complex authentication system or a simple form handler, this attribute helps create smooth, user-friendly experiences with minimal effort.

