# Token Generation

## Guiding Principles


When a user is granted authentication or authorization rights, a token—a randomly generated string—is created and stored in the `trongate_tokens` database table.


The `trongate_tokens` table contains a column named `user_id`, indicating that every generated token must be assigned to a specific user.


In the context of building large-scale web applications, a "user" could represent various entities, such as:


- A website administrator
- A record from a `members` table
- A record from a `trongate_administrators` table
- ...and more!


While your definition of a "user" may vary depending on the application's requirements, within Trongate's authentication and authorization framework, a "user" specifically refers to a record in the `trongate_users` table.


Therefore:


**When working with token-based authentication and authorization, every individual who requires a token must be represented in the `trongate_users` database table.**

> [!NOTE]
> **Just To Let You Know...**
>
> If the above explanation is unclear, don't worry—examples will be provided later in this chapter.



Token generation is a core feature of Trongate's authentication and authorization system, managed by the **Trongate Tokens** module. This module provides a robust mechanism for creating secure tokens that represent authenticated user sessions. At the heart of this process lies the _generate_token() method.


This method is responsible for generating unique tokens based on provided data. Below is the method signature and a detailed explanation of how it works:

```php
/**
 * Generate a token based on provided data.
 *
 * @param array $data An array containing token generation parameters.
 *   - 'user_id' (int) : required - The user's ID.
 *   - 'expiry_date' (int) : optional - Unix timestamp for token expiration.
 *   - 'set_cookie' (bool) : optional - If true, set the token as a cookie.
 *   - 'code' (string) : optional - Custom code for the token.
 *
 * @return string The generated token.
 */
public function _generate_token(array $data): string {
  // Generate a 32-character random string
  $random_string = make_rand_str();

  // Build data array variables (required for table insert)
  if (!isset($data['expiry_date'])) {
    $data['expiry_date'] = time() + $this->default_token_lifespan;
  }

  $data['token'] = $random_string;
  $params = $data;

  if (isset($params['set_cookie'])) {
    unset($params['set_cookie']);
  }

  $this->model->insert($params, 'trongate_tokens');

  if (isset($data['set_cookie'])) {
    setcookie('trongatetoken', $random_string, $data['expiry_date'], '/');
  } else {
    $_SESSION['trongatetoken'] = $random_string;
  }

  return $random_string;
}
```

### How It Works


The _generate_token() method performs the following steps:


1. **Generate a Random String:** A 32-character random string is created using the make_rand_str() helper function.
2. **Set Expiration Date:** If no expiration date is provided, the default lifespan of 86,400 seconds (1 day) is applied.
3. **Insert into Database:** The token details are inserted into the `trongate_tokens` table, associating the token with the specified user ID and expiration date.
4. **Store Token:** Depending on the `set_cookie` parameter, the token is either stored in a cookie or the session.
5. **Return Token:** The generated token is returned as a string for further use.

### Key Parameters


- **user_id** (required): Integer representing the user's ID in the `trongate_users` table.
- **expiry_date** (optional): Unix timestamp for token expiration. If omitted, the default lifespan of 86,400 seconds (1 day) is used.
- **set_cookie** (optional): Boolean to indicate if the token should be stored in a cookie. If not provided, the token is stored in the session.
- **code** (optional): String code for special access rights. Rarely used in manual token generation.

> [!NOTE]
> **Just To Let You Know...**
>
> If no expiration date is provided, the system uses a default lifespan, typically set to 86,400 seconds (1 day).
> 
> 
> The default token lifespan is declared at the top of the `Trongate_tokens` class, within the file named `Trongate_tokens.php`. You can modify the default token lifespan by changing the value assigned to `$default_token_lifespan`.
> 
> ```php
> <?php
> class Trongate_tokens extends Trongate {
> 
>     private $default_token_lifespan = 86400; // one day
> 
>     // rest of class...
> }
> ```


## Practical Examples of Token Generation


Below are practical examples of how tokens can be generated in various scenarios.

### Example 1: Generating a Token for a Specific User


To generate a token for a user with ID 88, expiring in one week:

```php
// Load the trongate_tokens module
$this->module('trongate_tokens');

// Prepare data array
$data = [
    'user_id' => 88, // ID from trongate_users table
    'expiry_date' => time() + (86400 * 7), // Token expires in 1 week
    'set_cookie' => true // Optional: set a cookie
];

// Generate the token
$token = $this->trongate_tokens->_generate_token($data);
```

### Example 2: Generating a Token Without Setting a Cookie


If you prefer to store the token in the session instead of a cookie, you can omit the `expiry_date` parameter, allowing the session's natural lifecycle to manage token expiration:

```php
// Load the trongate_tokens module
$this->module('trongate_tokens');

// Prepare data array
$data = [
    'user_id' => 88 // ID from trongate_users table
];

// Generate the token
$token = $this->trongate_tokens->_generate_token($data);
```


In this case, the token will automatically inherit the default lifespan of 86,400 seconds (1 day) unless otherwise configured.

> [!CAUTION]
> **Danger!**
>
> **Security Note:** In development mode ('dev'), Trongate will automatically generate and allocate a token for any user attempting to access the admin panel if no token is presented. This behavior is managed by the _make_sure_allowed() method in the 'Trongate Administrators' module.
> 
> 
> For production environments, ensure that the `ENV` constant in `config.php` is not set to 'dev' to avoid unintended token generation.


## In Summary


- Token generation in Trongate is handled by the `Trongate Tokens` module.
- Every token is assigned to a `user_id`.
- The `user_id` property refers to the `trongate_users` table.


In addition, tokens can be stored in multiple locations, including:


- **Session variables:** Ideal for server-side applications.
- **Cookies:** Useful for client-side persistence.
- **HTTP Headers:** Commonly used for API-based interactions.


When generating tokens, you have the option to:


1. Manually set an expiration date and time.
2. Allow the token lifespan to default to the `$default_token_lifespan`.

## Video Tutorial


Here's a video tutorial, walking you through how to build a private area using Trongate's token system.


https://www.youtube.com/watch?v=dGfkO9mU6DI

