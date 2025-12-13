# Token Validation

## Overview of Token Validation


The Trongate framework provides a robust mechanism for fetching and validating user tokens, which is crucial for implementing secure authentication and authorization in your applications.


Token validation is primarily handled by the [Trongate Tokens](../../reference/pre_installed/trongate_tokens) module, specifically through the _attempt_get_valid_token() method. This method validates tokens based on their existence in the database, their expiration status, and—most importantly—their association with specific user levels.

> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** The _attempt_get_valid_token() method validates tokens against user levels. If your application requires more granular validation (e.g., verifying a specific user ID), additional methods such as _get_user_id(), _get_user_obj(), or _get_user_level() can be used to enforce stricter conditions.


## The Mechanics of Token Retrieval


When an end user is allocated a 'Trongate token', the relevant details about the token are stored in the `trongate_tokens` database table. Upon subsequent visits to the application, the _attempt_get_valid_token() method can be used to retrieve and validate user tokens.


This method is versatile and adapts to various authentication scenarios by searching for tokens in multiple locations and applying optional user-level filters.

### Method Signature

```php
public function _attempt_get_valid_token($user_levels = null): string|bool
```

### Parameters


| Parameter | Type | Description | Default | Required |
| ---|---|---|---|---|
| `$user_levels` | int\|array\|null | User levels to filter tokens. | `null` | No |

### Return Value


The method returns either a string (the valid token) or a boolean `false` if no valid token is found.

## Token Retrieval Process


The _attempt_get_valid_token() method searches for tokens in the following locations, in order of priority:


1. HTTP headers (`$_SERVER['HTTP_TRONGATETOKEN']`)
2. Cookies (`$_COOKIE['trongatetoken']`)
3. Session (`$_SESSION['trongatetoken']`)


If a token is found in any of these locations, it is validated against the database to ensure it has not expired and matches the specified user-level criteria (if provided).

## How Validation Works


The validation process involves the following steps:


1. **Token Collection:** The method collects tokens from HTTP headers, cookies, and session variables.
2. **Database Query:** Each token is queried against the `trongate_tokens` table to verify its existence and expiration status.
3. **User-Level Filtering:** If user-level filtering is applied, the method ensures the token corresponds to a user with the required permissions.
4. **Return Valid Token:** If a valid token is found, it is returned; otherwise, the method returns `false`.

## Usage Examples

### Example 1: Fetching Any Valid Token


To retrieve a valid token for any user level:

```php
$this->module('trongate_tokens');
$token = $this->trongate_tokens->_attempt_get_valid_token(); // Any user level
```

### Example 2: Fetching Token for Specific User Level


To fetch a token for users with an 'admin' user level (assuming 'admin' has an ID of 1 in the `trongate_user_levels` table):

```php
$this->module('trongate_tokens');
$token = $this->trongate_tokens->_attempt_get_valid_token(1); // Admin only
```

### Example 3: Fetching Token for Multiple User Levels


To retrieve a token for users with either 'admin' or 'member' user levels (assuming IDs 1 and 2 respectively):

```php
$this->module('trongate_tokens');
$token = $this->trongate_tokens->_attempt_get_valid_token([1, 2]); // Admin or member
```

## Validating Tokens Against Custom Conditions


While the _attempt_get_valid_token() method is effective for validating tokens against user levels, some applications may require more granular validation. For example, you might need to ensure that a token corresponds to a specific user ID or other custom criteria. In such cases, you can use the following methods:

### Fetching the Trongate User ID


To validate a token against a specific user ID, use the _get_user_id() method. This method retrieves the Trongate User ID associated with a token:

```php
$this->module('trongate_tokens');
$user_id = $this->trongate_tokens->_get_user_id(); // Returns the user ID or false
```


If you have a specific token to validate, you can pass it as an argument:

```php
$this->module('trongate_tokens');
$user_id = $this->trongate_tokens->_get_user_id($token);
```

### Fetching the Trongate User Object


For more detailed user information, use the _get_user_obj() method. This method returns an object containing the user's data, including their user level, token, and expiration date:

```php
$this->module('trongate_tokens');
$user_obj = $this->trongate_tokens->_get_user_obj();

if ($user_obj) {
    echo "User Level: " . $user_obj->user_level;
    echo "User ID: " . $user_obj->trongate_user_id;
} else {
    echo "No valid token found.";
}
```

### Fetching the User Level


To validate a token against a specific user level, use the _get_user_level() method. This method retrieves the user level associated with a token:

```php
$this->module('trongate_tokens');
$user_level = $this->trongate_tokens->_get_user_level();

if ($user_level === 'admin') {
    echo "Access granted to admin.";
} else {
    echo "Access denied.";
}
```

## Security Considerations


When validating tokens, keep the following security considerations in mind:


- **Token Expiry:** Ensure that tokens have a reasonable lifespan to minimize the risk of unauthorized access.
- **Secure Storage:** Use HTTPS to protect tokens transmitted via HTTP headers or cookies.
- **Granular Validation:** For sensitive operations, combine token validation with additional checks, such as verifying the user ID or role.

> [!WARNING]
> The Trongate Tokens module employs a hierarchical mechanism to fetch valid tokens during authentication and authorization processes. This mechanism involves sequentially checking multiple storage locations for tokens, as outlined below:
> 
> 
> 1. **HTTP Headers:** The framework first attempts to retrieve a token from the HTTP headers (`$_SERVER['HTTP_TRONGATETOKEN']`).
> 2. **Cookies:** If no token is found in the headers, the framework proceeds to check for a token stored as a cookie (`$_COOKIE['trongatetoken']`).
> 3. **Session Data:** Finally, if no token is located in the headers or cookies, the framework attempts to retrieve a token from session data (`$_SESSION['trongatetoken']`).
> 
> 
> This sequential retrieval process ensures that the framework can locate and validate tokens stored in various locations, thereby enabling seamless user authentication and authorization.
> 
> 
> Developers should be aware that the removal of token data from one location (e.g., cookies) does not automatically eliminate tokens stored elsewhere (e.g., session data). Consequently, incomplete token cleanup may lead to unintended persistence of user sessions.
> 
> 
> To ensure comprehensive token deletion—both from the user's device and the application's database—developers are encouraged to utilize the _destroy() method. This method systematically removes tokens from all storage locations and purges them from the database, thereby maintaining a secure and consistent state.


## In Summary


The _attempt_get_valid_token() method is a powerful tool for retrieving and validating user tokens in Trongate applications. While it excels at validating tokens against user levels, additional methods like _get_user_id(), _get_user_obj(), and _get_user_level() allow for more granular validation when needed. By leveraging these tools effectively, developers can implement secure and flexible authentication and authorization workflows.

