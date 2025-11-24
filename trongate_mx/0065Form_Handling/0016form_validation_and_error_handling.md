# Form Validation and Error Handling


Displaying form validation errors with Trongate MX is an easy two-step process.

### Step 1


- Add a class of `highlight-errors` to your opening form tag.

### Step 2


- Modify your endpoint so that it invokes `echo validation_errors(xxx);` when validation errors occur.


**NOTE:** When invoking validation_errors(), replace `xxx` with an appropriate error status code, such as **400**.


---

## Understanding Different Types of Form Responses


Trongate MX handles form submissions differently based on the HTTP status code returned by the server:

### Form Validation Errors (400, 422, etc.)


When validation errors occur and the form has the `highlight-errors` class, Trongate MX will:


- Parse the JSON response containing validation errors
- Display these errors inline next to the relevant form fields
- Handle the response according to normal validation error protocols

### Security-Related Responses (401, 402, 403)


For security-related status codes (unauthorized, payment required, or forbidden), Trongate MX will:


- Skip the validation error handling process
- Allow other error handling attributes like `mx-redirect-on-error` or `mx-on-error` to take effect


This means you can handle authentication failures, session timeouts, or CSRF protection failures using standard Trongate MX attributes. For example:

```html
<form class="highlight-errors" 
      mx-post="users/update_profile"
      mx-redirect-on-error="true">
    <!-- form fields here -->
</form>
```


If the server returns a 401 status code (e.g., due to an expired session), Trongate MX will process the redirect instead of trying to display validation errors. Similarly, you could use `mx-on-error` to display a custom "Session Expired" message.

## Video Tutorial


Below is a short video tutorial demonstrating how to add form validation errors when working with Trongate MX.


https://www.youtube.com/watch?v=Lb_gjo5tlnk

## Tutorial Resources


The starter code for the video tutorial is available on GitHub. Click the button below to access the repository and download the starter code.


[Get Starter Code](https://github.com/trongate/trongate_mx_validation_tutorial)

## Prerequisites


To use Trongate's built-in form validation features with Trongate MX, ensure your webpage includes the following:


1. A `base` element inside the `<head>` section with its value set to your website's base URL.
2. A `link` element inside the `<head>` section that loads `trongate.css`.
3. Opening and closing `script` tags with the `src` attribute pointing to `js/trongate-mx.js`. *

> [!NOTE]
> **Just To Let You Know...**
>
> * The `script` tag for loading Trongate MX can be placed **either** in the `<head>` section or just before the closing `</body>` tag.



Here's an example of a basic HTML template ready to work with Trongate MX:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <base href="<?= BASE_URL ?>">
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="css/trongate.css">
  <script src="js/trongate-mx.js"></script>
  <title>Document</title>
</head>
<body>
  <h1>Ready To Rock!</h1>
  <p>This page is locked, loaded and ready to work with Trongate MX.</p>
</body>
</html>
```

> [!WARNING]
> **Warning!**
>
> When using Trongate's [Validation class](documentation-ref/list_refs/class_reference/the-validation-class) for form validation, ensure your forms are closed with:
> 
> ```vf
> echo form_close();
> ```
> 
> 
> This is essential because Trongate's [Validation class](documentation-ref/list_refs/class_reference/the-validation-class) automatically applies CSRF protection to all incoming requests. Using form_close() *not only* generates a closing form tag but also creates the necessary security token required for Trongate's CSRF protection mechanisms.
> 
> 
> Failing to use form_close() will result in rejected requests due to Trongate's stringent security protocols.


## Summary


The ability to dynamically render inline form validation errors with just two lines of code is arguably one of Trongate MX's most impressive features.


Ask yourself:


**"How long would it take to build this kind of functionality *without* Trongate MX?"**


Even for an experienced developer, building such functionality would almost certainly take several hours or would require depending upon third-party libraries.


What truly sets Trongate MX apart is that it allows you to leverage Trongate's [Validation class](documentation-ref/list_refs/class_reference/the-validation-class), security features, and form helpers - all out of the box. *Not only* can you build beautiful, highly interactive single-page applications without writing JavaScript, but you can also do so *without* relying on any third-party libraries!

## And there's more!


With Trongate MX, it's also possible to invoke your own custom JavaScript functions after validation errors have occurred.  Full details on how to take advantage of this functionality are covered on the next page.

