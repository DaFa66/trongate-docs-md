# CSRF Protection


Cross-Site Request Forgery (CSRF) is a type of security vulnerability that allows malicious websites to execute unwanted actions on behalf of authenticated users. This attack occurs when a user visits a malicious website while being authenticated on another site, and the malicious site tricks the user's browser into making unwanted requests to the legitimate site.

## How CSRF Attacks Work


Consider these common scenarios:


1. **Financial Attack:**
- You log into your bank account and stay logged in.
- In another tab, you visit a malicious website.
- The malicious site contains hidden code that sends a request to your bank to transfer money.
- Since you're still authenticated with your bank, the request includes your valid session cookie.
- The bank processes the request because it appears legitimate.


2. **Form Submission Attack:**
- You're logged into your website's admin panel.
- A malicious user sets up a fake form on their website that matches your site's form structure.
- They trick you into submitting their form (maybe disguised as something else).
- The form submits to your website, carrying your valid authentication.
- Your website processes the unwanted form submission.



## Built-in Protection in Trongate MX


Trongate provides robust CSRF protection out of the box through its Validation class and form helpers. The framework uses a token-based approach where:


- A unique CSRF token is generated for each form.
- The token is included in the form as a hidden field.
- The Validation class verifies this token when processing form submissions.
- If the token is missing or invalid, the request is blocked.

## Implementing CSRF Protection


To implement CSRF protection in your Trongate MX applications, you need two key ingredients:

### 1. Use the Validation Class


The Validation class automatically includes CSRF protection for all form submissions. This ensures that form submissions are only accepted from your legitimate website.

### 2. Use form_close() Helper


The form_close() helper function is crucial for CSRF protection as it automatically generates and includes a CSRF token in your forms. Here's a complete example:

```php
<?php 
$form_attr = [
    'mx-post' => 'users/create',
    'mx-target' => '#response'
];
echo form_open('#', $form_attr);
echo form_label('Username');
echo form_input('username', '');
echo form_label('Email');
echo form_input('email', '');
echo form_submit('submit', 'Create Account');
echo form_close();
?>
<div id="response"></div>
```


The above code generates HTML that includes a hidden CSRF token:

```html
<form mx-post="users/create" mx-target="#response">
    <label>Username</label>
    <input type="text" name="username" value="">
    <label>Email</label>
    <input type="text" name="email" value="">
    <button type="submit" name="submit">Create Account</button>
    <input type="hidden" name="csrf_token" value="generated_secure_token_here">
</form>
<div id="response"></div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> For more information about form handling with Trongate MX, refer to the [Form Handling Overview](../0065Form_Handling/0010form_handling_overview.md).


## How It Works Behind the Scenes


When you use form_close(), Trongate:


1. Generates a secure random token using `random_bytes(32)`.
2. Stores the token in the user's session.
3. Adds the token to the form as a hidden field.


When the form is submitted, the Validation class:


1. Checks for the presence of the CSRF token in the request data.
2. Compares it with the token stored in the session.
3. Blocks the request if the tokens don't match or if the token is missing.
4. Uses `hash_equals()` for secure string comparison to prevent timing attacks.

> [!NOTE]
> **Just To Let You Know...**
>
> Always use form_close() and Trongate's [Validation class](documentation-ref/list_refs/class_reference/the-validation-class) when working with forms in Trongate MX. These two elements provide automatic CSRF protection and helps prevent security vulnerabilities.


## Automatic Protection


CSRF protection in Trongate MX is automatic when you follow these best practices:


- Use form_close() to properly close your forms and generate CSRF tokens.
- Process form submissions through the Validation class.
- Use POST method for state-changing operations.

> [!NOTE]
> **Just To Let You Know...**
>
> - CSRF tokens are automatically regenerated for each form.
> - Tokens are session-specific and can't be used across different sessions.
> - CSRF protection is mandatory for all POST requests processed by the Validation class.


## Best Practices


While Trongate MX handles CSRF protection automatically, following these best practices will ensure maximum security:


- Always use POST (not GET) for state-changing operations.
- Keep forms within a single page (avoid storing form data across multiple pages).
- Don't disable or bypass the built-in CSRF protection.
- Use HTTPS to prevent token theft via man-in-the-middle attacks.
- Keep your Trongate framework updated to get the latest security improvements.

> [!WARNING]
> At the time of writing, Trongate MX is able to apply automatic CSRF protection to API endpoints where:
> 
> 
> 1. A form has been submitted.
> 2. Trongate's [Validation class](documentation-ref/list_refs/class_reference/the-validation-class) is being used to validate submitted form data.
> 
> 
> Of course, it's possible that you may wish to have CSRF protection applied to endpoints that neither handle form submissions nor make use of Trongate's [Validation class](documentation-ref/list_refs/class_reference/the-validation-class). For those kinds of situations, you'll have to write your own custom CSRF protection solution.
> 
> 
> Such a solution would involve generating a unique token for each session or request, storing it securely (e.g., in a session or a database), and ensuring that the token is sent along with requests that modify server-side data. You would then validate the token on the server before processing any sensitive actions to ensure that the request is legitimate and not forged.
> 
> 
> At the time of writing, this kind of functionality has not been built into Trongate MX. However, if it's something that you think would add value to Trongate MX, [let us know](https://trongate.io/contactus). If enough people ask for a feature, we'll build it!


