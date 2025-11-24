# Custom Headers


The `mx-headers` attribute allows you to add custom HTTP headers to your Trongate MX requests. This feature is particularly useful when you need to send additional information to your server endpoints, such as authentication tokens, API keys, or custom metadata.

## Basic Usage


The `mx-headers` attribute accepts a JSON object containing key-value pairs that represent your custom headers. Each key-value pair will be sent as an HTTP header with your request.


Here's a basic example using Trongate's form_button() helper function:

```vf
<?php
$auth_token = 'abc123'; // Example token
$btn_attr = [
    'mx-get' => 'api/protected_data',
    'mx-target' => '#result',
    'mx-headers' => '{"Authorization": "Bearer '.$auth_token.'", "Custom-Header": "custom-value"}'
];
echo form_button('fetch_btn', 'Fetch Protected Data', $btn_attr);
?>

<div id="result"></div>
```


And here's the equivalent using pure HTML:

```html
<button mx-get="api/protected_data" 
        mx-target="#result" 
        mx-headers='{"Authorization": "Bearer abc123", "Custom-Header": "custom-value"}'>
    Fetch Protected Data
</button>

<div id="result"></div>
```

> [!CAUTION]
> **Danger!**
>
> The example above is for illustration purposes only. **Never** hardcode security tokens or API keys directly into HTML source code. These credentials would be visible in the page source and could pose significant security risks.


## Cleaner Syntax for Advanced Use


To avoid syntax errors and improve maintainability when working with multiple headers, you can combine Trongate's form_button() function with PHP's `json_encode()`:

```vf
<?php 
$auth_token = 'abc123'; // Example token
$client_id = 'client-5678'; // Example client ID

$headers = [
    'Authorization' => 'Bearer ' . $auth_token,
    'X-API-Version' => '2.0',
    'X-Client-ID' => $client_id,
    'Accept-Language' => 'en-US,en;q=0.9',
    'X-Request-Source' => 'WebApp'
];

$attributes = [
    'mx-get' => 'api/protected_data',
    'mx-target' => '#result',
    'mx-headers' => json_encode($headers)
];
echo form_button('fetch_btn', 'Fetch Protected Data', $attributes);
?>
```


This approach uses PHP's `json_encode()` function to ensure properly formatted JSON for the `mx-headers` attribute while keeping the code maintainable.


For those who prefer to work primarily with HTML, here's an alternative syntax:

```vf
<button mx-get="api/protected_data"
        mx-target="#result"
        mx-headers='{
            "Authorization": "Bearer <?= $auth_token ?>",
            "X-API-Version": "2.0",
            "X-Client-ID": "<?= $client_id ?>",
            "Accept-Language": "en-US,en;q=0.9",
            "X-Request-Source": "WebApp"
        }'>
    Fetch Protected Data
</button>
```

## Important Technical Considerations

> [!NOTE]
> **Just To Let You Know...**
>
> - The `mx-headers` value must be valid JSON - malformed JSON will cause the request to fail
> - When using HTML attributes directly, use single quotes around the attribute value since JSON requires double quotes for properties
> - Header names are case-insensitive according to the HTTP specification, but conventionally written in Title-Case
> - Some headers (like `Content-Length`) are automatically managed by browsers and cannot be set via JavaScript


## Common Use Cases

### 1. Authentication Headers


Authentication is a primary use case for custom headers. Here's a secure implementation using the form_button() function:

```vf
<?php
$token = get_session_token(); // Get token from your session management system
$btn_attr = [
    'mx-post' => 'api/secure_endpoint',
    'mx-target' => '#secure-content',
    'mx-headers' => json_encode([
        'Authorization' => 'Bearer ' . $token
    ])
];
echo form_button('secure_btn', 'Access Secure Content', $btn_attr);
?>
```

> [!NOTE]
> **Just To Let You Know...**
>
> **Authentication Best Practices:**
> 
> 
> - Use `Bearer` authentication for JWTs and OAuth 2.0 access tokens
> - Implement CSRF protection for POST requests
> - Store tokens securely (e.g., in HTTP-only cookies for session tokens)
> - Use short-lived tokens and implement proper token rotation


### 2. API Version Headers


Version headers help manage API compatibility:

```html
<button mx-get="api/data" 
        mx-target="#api-result" 
        mx-headers='{
            "Accept": "application/json",
            "X-API-Version": "2.0"
        }'>
    Fetch Data
</button>
```

### 3. Request Tracking Headers


Custom headers can help with request tracking and debugging:

```vf
<?php
$headers = [
    'Authorization' => 'Bearer ' . $token,
    'X-Request-ID' => uniqid(),
    'X-Client-Version' => APP_VERSION,
    'X-Device-Type' => 'web'
];

$btn_attr = [
    'mx-get' => 'api/tracked_request',
    'mx-target' => '#tracking-result',
    'mx-headers' => json_encode($headers)
];
echo form_button('track_btn', 'Tracked Request', $btn_attr);
?>
```

## Security Considerations

> [!WARNING]
> **Warning!**
>
> **Critical Security Guidelines:**
> 
> 
> - Always use HTTPS for requests containing sensitive headers
> - Validate and sanitize all header values on both client and server sides
> - Store sensitive tokens securely
> - Implement rate limiting on endpoints that accept custom headers


## Conclusion


The `mx-headers` attribute provides a flexible way to include custom HTTP headers in your Trongate MX requests. When implemented with proper security considerations, it enables robust authentication, versioning, and request tracking capabilities in your applications.

