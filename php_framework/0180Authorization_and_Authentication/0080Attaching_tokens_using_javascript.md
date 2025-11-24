# Attaching Tokens to HTTP Requests

## Overview


When interacting with Trongate API endpoints, it is essential to include the Trongate token in the HTTP request headers for authentication. This ensures that the server can validate the user's identity and authorize access to protected resources. Below are demonstrations of how to attach a Trongate token to HTTP requests using JavaScript, specifically with `XMLHttpRequest` and the modern `Fetch API`.

> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** The Trongate token should be included in the `trongateToken` header for all authenticated requests. Ensure that the token is securely stored and transmitted over HTTPS to prevent unauthorized access.


## Using XMLHttpRequest


The `XMLHttpRequest` object provides a traditional way to send HTTP requests in JavaScript. Below is an example of how to attach a Trongate token to the request headers using this approach:

```javascript
const targetUrl = 'your_base_url/trongate_tokens/id';
const token = 'your_trongate_token'; // Replace with your actual Trongate token
const http = new XMLHttpRequest();

http.open('GET', targetUrl);
http.setRequestHeader('Content-type', 'application/json');
http.setRequestHeader('trongateToken', token);
http.send();

http.onload = function() {
  console.log(http.status); // Logs the HTTP status code (e.g., 200 for success)
  console.log(http.responseText); // Logs the response from the server
};
```

### Explanation


- **targetUrl:** Replace this with the actual URL of the Trongate API endpoint you wish to interact with.
- **token:** Replace this placeholder with the actual Trongate token generated for the user.
- **setRequestHeader:** The `trongateToken` header is explicitly set to include the token for authentication.
- **onload:** This event handler processes the server's response once the request is complete.

## Using Fetch API


The `Fetch API` offers a more modern and promise-based approach to making HTTP requests. Below is an example of how to attach a Trongate token to the request headers using the `Fetch API`:

```javascript
const targetUrl = 'your_base_url/trongate_tokens/id';
const token = 'your_trongate_token'; // Replace with your actual Trongate token

fetch(targetUrl, {
  method: 'GET',
  headers: {
    'Content-Type': 'application/json',
    'trongateToken': token,
  },
})
  .then((response) => response.json()) // Parse the JSON response
  .then((data) => console.log(data)) // Log the parsed data
  .catch((error) => console.error('Error:', error)); // Handle any errors
```

### Explanation


- **targetUrl:** Replace this with the actual URL of the Trongate API endpoint you wish to interact with.
- **token:** Replace this placeholder with the actual Trongate token generated for the user.
- **headers:** The `trongateToken` header is included in the request to authenticate the user.
- **Promises:** The `Fetch API` uses promises to handle asynchronous operations, making it easier to manage responses and errors.

> [!TIP]
> **Best Practices**
>
> Developers who are using [Trongate MX](documentation/display/trongate_mx) are advised to use the 'mx-token' attribute to automatically add token data to HTTP requests.  For more information, [click here](documentation/display/trongate_mx/trongate-mx-security/working-with-trongate-tokens).


## Fetching Tokens from HTTP Headers Using Pure PHP


In server-side PHP code, tokens sent via HTTP headers can be accessed directly using the `$_SERVER` superglobal. For example:

```php
$token = $_SERVER['HTTP_TRONGATETOKEN'] ?? false;
```


In the code sample above, a `$token` variable is assigned the value of a 'Trongate token' passed via an HTTP request header. If no such header is found, the `$token` variable will be assigned a boolean value of `false`.

> [!WARNING]
> **Warning!**
>
> Accessing token data from the header via the `$_SERVER` superglobal does not confirm whether the token passed via the header is valid.
> 
> 
> To validate token data, refer to the [token validation documentation](documentation/display/php_framework/authorization-and-authentication/token-validation) for guidance on using the Trongate Tokens class.


## Security Considerations


When attaching tokens to HTTP headers, keep the following security considerations in mind:


- **HTTPS:** Always transmit tokens over HTTPS to encrypt the data and prevent interception by malicious actors.
- **Token Storage:** Store tokens securely on the client side. For web applications, consider using secure cookies or session storage to minimize exposure.
- **Token Expiry:** Ensure that tokens have a reasonable lifespan and implement mechanisms to refresh or regenerate them as needed.
- **Error Handling:** Implement robust error handling to detect and respond to failed authentication attempts or expired tokens.

