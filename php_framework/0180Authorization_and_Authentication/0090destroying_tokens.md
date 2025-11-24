# Destroying Tokens


In certain scenarios, such as when a user logs out of a private members' area, it may be necessary to delete a token from the user's device and from your application's database. This can be accomplished by invoking the _destroy() method from the **Trongate Tokens** module. This method does not require any arguments.

## How It Works


The _destroy() method systematically removes tokens from the following possible storage locations:


- **Session Data:** If a token is stored in the session, it will be cleared.
- **Cookies:** If a token is stored as a cookie, it will be deleted from the user's browser.
- **Database Records:** Any corresponding records in the `trongate_tokens` table will be removed.


This ensures that the token is completely invalidated and cannot be reused for authentication or authorization purposes.

## Example Usage


Below is an example of how to invoke the _destroy() method:

```php
$this->module('trongate_tokens');
$this->trongate_tokens->_destroy();
```
### Explanation


- **Line 1:** Loads the `trongate_tokens` module, making its methods available for use.
- **Line 2:** Invokes the _destroy() method to clear tokens from the session, cookies, and database.

> [!NOTE]
> **Just To Let You Know...**
>
> This method clears any tokens that might be stored as either session data or cookie data on the user's device. If a token is found, the method will also delete corresponding records from the `trongate_tokens` table.
> 
> 
> If the _destroy() method is invoked when the end user does *not* have a valid token, nothing will happen, and no error messages will be produced.


## Security Implications


Properly destroying tokens is a critical aspect of maintaining application security. By invoking the _destroy() method during logout or other relevant events, you ensure that:


- **Session Termination:** The user's session is terminated, preventing unauthorized access to protected resources.
- **Token Cleanup:** Tokens are removed from both the client side (session or cookies) and the server side (database), minimizing the risk of token reuse or hijacking.

## Additional Considerations


While the _destroy() method handles token cleanup comprehensively, developers should also consider the following best practices:


- **Logout Confirmation:** Provide users with feedback (e.g., a success message) after invoking the _destroy() method to confirm that they have been logged out.
- **Redirect After Logout:** Redirect users to a public page (e.g., the login screen or homepage) after destroying their tokens to prevent accidental re-access to restricted areas.
- **Token Expiry:** Ensure that tokens have a reasonable lifespan and implement mechanisms to automatically expire and clean up unused tokens from the database.

