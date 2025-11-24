# Working with Trongate Tokens


The `mx-token` attribute in Trongate MX provides a mechanism for seamlessly integrating Trongate's authentication and authorisation system by attaching Trongate Tokens to outgoing HTTP requests.

## Implementation Overview


The Trongate PHP framework includes a powerful module named `trongate_tokens`. This module facilitates authentication and authorisation tasks, enabling you to secure API endpoints with customisable rules. With the `trongate_tokens` module, you can enforce granular control over who can interact with your API.

> [!NOTE]
> **Just To Let You Know...**
>
> Trongate's authorisation system supports a variety of access control patterns. Examples of possible API authorisation rules are:
> 
> 
> 1. Allow access to an API endpoint for users who **have a user level of 'admin'**.
> 2. Allow access to an API endpoint for users who **either have a user level of 'admin' or a user level of 'member'**.
> 3. Allow access to an API endpoint for **any logged in user**.
> 4. Allow access to an API endpoint for **users who signed up within the last half hour**.


## What Are 'Trongate Tokens'?


Trongate Tokens are unique, cryptographically generated strings managed by the `trongate_tokens` module. These tokens act as secure identifiers for users within your application, enabling robust stateful authentication mechanisms. Below is an example of a Trongate Token:

```
JzMSngd6VJhYzzcXCKyatoYQr8SbpjzN
```

> [!NOTE]
> **Just To Let You Know...**
>
> With a valid Trongate Token, you can:
> 
> 
> 1. Verify if a user is authenticated
> 2. Retrieve associated user details, such as:
> 	    
> - Username
> - Email address
> - User role/level
> - Additional user metadata


## Using Trongate Tokens With Trongate MX


Developers working with Trongate MX can easily take advantage of Trongate's inbuilt token-based security system.


Usage revolves around a three-step process:


1. Attach a Trongate Token to an element that triggers an HTTP response.
2. Attempt to read a submitted token from your API endpoint.
3. Have your API endpoint grant or deny access based on the presence or absence of a valid Trongate Token.


Let's go through each of these three steps, one at a time.


---

## 1: Attaching Tokens to Elements


To attach a Trongate Token to an element, we need to first attempt to fetch a valid Trongate Token using PHP. This can be achieved by loading the 'trongate_tokens' module and invoking the _attempt_get_valid_token() method. For example:

```php
$this->module('trongate_tokens');
$token = $this->trongate_tokens->_attempt_get_valid_token();
```

### Passing The Token Into The View File


Having fetched a Trongate Token, our next task is to pass the fetched token into the associated view file. It's worth noting that the _attempt_get_valid_token() method will return a boolean of **false** if no valid token is found for the user. With that being the case, it's a good idea to make sure the value of your token is a (variable of a type) *string* - regardless of the response from the 'trongate_tokens' module. This can be achieved by using PHP's `settype()` function. For example:

```php
settype($token, 'string');
$data['trongate_token'] = $token;
```


The lines of code, shown above, achieve two things:


1. They convert the value of `$token` to a type of string.
2. They add the value of the token onto a `$data` array - giving it a property of 'trongate_token'.


As is normal practice, with Trongate, your corresponding view file or template can then be loaded having the `$data` array passed in. For example:

```php
$this->template('public', $data);
```

### Accessing The Token From The View File


Having fetched a token and passed it into your view file, your Trongate Token should now be available via a `$trongate_token` variable.


As a reminder, if you failed to fetch a valid token for the user then the value for `$trongate_token` will be an empty string (since we used `settype()` in the controller file).

### Appending The Token To An Element


We can then attach the fetched Trongate Token (which may or may not be a valid token) to an HTML element using the `mx-token` attribute. For example,

```vf
<?php
$attr = [
    'mx-get' => 'api/protected_resource',
    'mx-token' => $trongate_token
];

echo form_button('Fetch Protected Resource', $attr);
?>
```


If you prefer working with a more HTML-centered syntax, the same result can be achieved with:

```vf
<button mx-get="http://localhost/api/protected_resource" 
        mx-token="<?= $trongate_token ?>">
    Fetch Protected Resource
</button>
```


Regardless of whether or not you choose to use Trongate's form helper functions the result will be the same - any HTTP request that gets invoked by clicking on the button will have a Trongate Token attached to the request header.

> [!NOTE]
> **Just To Let You Know...**
>
> ### Understanding HTTP Request Headers
> 
> 
> HTTP request headers are key-value pairs sent with every HTTP request that provide essential information about the request being made. They act like metadata that helps both the client and server better understand and process the communication.
> 
> 
> Request headers serve multiple purposes:
> 
> 
> - They can provide context about the request (like what type of browser is making it)
> - They can specify how the server should respond (such as preferred content format)
> - They can contain authentication and security information
> - They can help to manage caching behavior
> 
> 
> Accessing header values depends on your environment. In most PHP setups, you can use `getallheaders()` or the `$_SERVER` superglobal to access HTTP headers.
> 
> 
> With Trongate, you can render an array of headers information with:
> 
> ```php
> json($_SERVER);
> ```


## 2: Fetching Sent Tokens From The API


Having attached a Trongate Token onto your request header, the next task is to have your API endpoint *fetch* the Trongate Token from the header.


There's actually two ways to do this:


1. By using the Trongate Tokens module.
2. By using pure PHP.


Let's go through both of these options.

### Fetching Tokens Using The Trongate Tokens Module


If you've been following along with this example, you'll know that we used the Trongate Tokens module to (attempt to!) fetch a Trongate Token which could *then* be passed into a view file and - ultimately - attached to an HTTP request.


You can use the same methodology to fetch the token from your API endpoints. Here's a reminder of the syntax:

```php
$this->module('trongate_tokens');
$token = $this->trongate_tokens->_attempt_get_valid_token();
```

> [!WARNING]
> **Warning!**
>
> The _attempt_get_valid_token() method, within the Trongate Tokens module, attempts to return a Trongate Token for a signed in user by checking:
> 
> 
> 1. The request headers
> 2. The user's session data
> 3. The user's cookie data
> 
> 
> That's three different places where Trongate Tokens can potentially be stored for any given user.
> 
> 
> This means that there's a hypothetical possibility of _attempt_get_valid_token() returning a false positive (i.e., signifying a user to be logged in) *even if* the user has failed to successfully attach a valid token to the HTTP request.
> 
> 
> In a live situation this is unlikely to be a problem. In a development environment, however, it could make the job of testing API endpoints quite difficult.


### Fetching Tokens Using Pure PHP


Instead of using the Trongate Tokens module to attempt to fetch the Trongate Token from the header, you can use pure PHP. This can be achieved with the following:

```php
$trongate_token = $_SERVER['HTTP_TRONGATETOKEN'];
```


Of course, this is not a perfect solution since an error would be thrown in instances where a Trongate Token has *not* been attached to the HTTP request header.


This can be mitigated by using the ternary operator. For example, with the code below, we attempt to read a Trongate Token from an HTTP request header. However, if a token is not found in the header, the `$trongate_token` value will be assigned with an empty string.

```php
$trongate_token = $_SERVER['HTTP_TRONGATETOKEN'] ?? '';
```

> [!NOTE]
> **Just To Let You Know...**
>
> ### Learning More About Trongate's Token System
> 
> 
> A full, in-depth explanation of Trongate's Token based security system is beyond the scope of the documentation for Trongate MX. However, if you require more information about this topic, please refer to: [How Trongate's Token System Works](https://trongate.io/dox/information/how-trongates-token-system-works).



With the assumption that you know how to authenticate a user, based on the presence or lack of a valid Trongate Token, it's then for you - the developer - to decide whether or not to grant or allow access to an API endpoint.

## Granting Or Denying API Access


Once you've validated (or invalidated) a Trongate Token, your API endpoint should respond appropriately using standard HTTP response codes. Here's how to handle common scenarios:

### Successful Access


When a valid token is provided and meets all authorization requirements, your endpoint should return an HTTP response code within the success range.  For example:

```php
http_reponse_code(200);
```


Example of granting access:

```php
public function protected_endpoint() {
    $token = $_SERVER['HTTP_TRONGATETOKEN'] ?? '';
    
    if ($this->_validate_token($token)) {
        http_response_code(200);
        echo json_encode(['message' => 'Access granted', 'data' => $your_data]);
    }
}
```

### Access Denied


When access needs to be denied, use appropriate status codes to indicate why.  Examples include but are not limited to the following:


- HTTP 401 (Unauthorized) - When no token is provided or the token is invalid
- HTTP 403 (Forbidden) - When the token is valid but the user lacks sufficient permissions
- HTTP 429 (Too Many Requests) - When rate limiting is exceeded


Example of denying access:

```php
public function protected_endpoint() {
    $token = $_SERVER['HTTP_TRONGATETOKEN'] ?? '';
    
    if (!$token) {
        http_response_code(401);
        echo json_encode(['error' => 'No authorization token provided']);
        die();
    }
    
    if (!$this->_validate_token($token)) {
        http_response_code(401);
        echo json_encode(['error' => 'Invalid token']);
        die();
    }
    
    if (!$this->_check_user_permissions($token)) {
        http_response_code(403);
        echo json_encode(['error' => 'Insufficient permissions']);
        die();
    }
}
```

> [!TIP]
> **Best Practices**
>
> When implementing token-based access control:
> 
> 
> 1. Always use appropriate HTTP status codes to indicate the result
> 2. Include clear error messages in the response body
> 3. Log failed access attempts for security monitoring
> 4. Consider implementing rate limiting for your API endpoints
> 5. Use environment variables for any sensitive configuration



Remember that proper error handling and clear response messages help both security and developer experience. Your API should be both secure and user-friendly.

