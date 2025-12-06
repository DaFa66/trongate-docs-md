# HTTP Methods in Trongate MX


Trongate MX provides a set of attributes that allow you to make various types of HTTP requests directly from your HTML elements. These attributes correspond to different HTTP methods and enable you to create dynamic, interactive web applications with minimal JavaScript.

## Available HTTP Method Attributes


Trongate MX supports the following HTTP method attributes:


- `mx-get`: For making GET requests
- `mx-post`: For making POST requests
- `mx-put`: For making PUT requests
- `mx-patch`: For making PATCH requests
- `mx-delete`: For making DELETE requests

> [!NOTE]
> **Just To Let You Know...**
>
> Trongate MX fully supports REST-style HTTP request methods like **PUT**, **PATCH**, and **DELETE**. However, these methods are entirely **optional**. Many developers choose to rely on **GET** and **POST** requests - a trusted and effective standard within the PHP ecosystem.


## HTTP Method Attributes at a Glance


The table below shows all of the different types of HTTP requests that can be made with Trongate MX, along with their corresponding 'MX attributes' and typical use cases.


| Attribute | HTTP Method | Typical Use |
| ---|---|---|
| `mx-get` | GET | Retrieve data |
| `mx-post` | POST | Submit new data |
| `mx-put` | PUT | Update existing data |
| `mx-patch` | PATCH | Partially update data |
| `mx-delete` | DELETE | Delete data |

> [!NOTE]
> **Just To Let You Know...**
>
> ### How Trongate MX Handles HTTP Methods
> 
> 
> Trongate MX provides flexible handling of various HTTP methods:
> 
> 
> 1. **Client-Side (Trongate MX):**
> - The JavaScript library supports all HTTP method attributes (`mx-get`, `mx-post`, `mx-put`, `mx-patch`, `mx-delete`).
> - Sends requests using the specified HTTP method.
> 
> 
> 2. **Server-Side (Trongate PHP):**
> - Check the HTTP method using: `$_SERVER['REQUEST_METHOD']`.
> - Get request data using the post() function, which handles all HTTP methods.
> 
> 
> 
> #### Example Usage in Controllers:
> 
> ```php
> $method = $_SERVER['REQUEST_METHOD'];
> $data = post('field_name', true);
> 
> switch ($method) {
>   case 'GET':
>     // Handle data retrieval
>     break;
>   case 'POST':
>     // Handle new data submission
>     break;
>   case 'PUT':
>     // Handle update
>     break;
>   case 'PATCH':
>     // Handle partial update
>     break;
>   case 'DELETE':
>     // Handle deletion
>     break;
> }
> ```
> 
> 
> **What this means for you:** You can use any HTTP method attribute in your HTML when making requests. On the server side, use `$_SERVER['REQUEST_METHOD']` to determine the HTTP method and post() to get the request data.


## Basic Usage


To use these attributes, simply add them to your HTML elements with the URL you want to request as the value.

### GET Request Example

```vf
<?php
$attributes = [
  'mx-get' => 'api/get_data',
  'mx-target' => '#result'
];
echo form_button('get_data_btn', 'Get Data', $attributes);
?>

<div id="result"></div>
```


Here's an alternative syntax, for those who prefer to work with pure HTML:

```html
<button mx-get="api/get_data" 
        mx-target="#result">Get Data</button>

<div id="result"></div>
```


When the button is clicked, an HTTP GET request is sent to 'api/get_data'. The response will be displayed in the element with id="result".

> [!TIP]
> **Best Practices**
>
> Remember to include a `<base>` tag in your webpage's head section:
> 
> ```html
> <base href="<?= BASE_URL ?>">
> ```


### Post Request Example


The code below demonstrates how to invoke an HTTP POST request, when a button in clicked, using Trongate MX:

```vf
<?php
$attributes = [
  'mx-post' => 'form/submit',
  'mx-target' => '#form-result'
];
echo form_button('submit_btn', 'Submit', $attributes);
?>

<div id="form-result"></div>
```


Here's an alternative syntax for those who prefer to use pure HTML:

```html
<button mx-post="forms/submit" mx-target="#form-result">Submit</button>

<div id="form-result"></div>
```


The code above would produce a button that has the text, 'Submit'.   For example:


Submit


Clicking on the 'Submit' button would invoke an HTTP POST request which would be sent to a URL of the following form:

```
<base-url>form/submit
```

> [!NOTE]
> **Just To Let You Know...**
>
> You may assume that `<base-url>` would be replaced by the base URL of your web application.  In reality, this means that your target URL may be more like this:
> 
> ```
> https://example.com/form/submit
> ```



Once a response is received from the API endpoint (at 'form/submit'), the response text would then be displayed inside a div with an 'id' of 'form-result'.

> [!TIP]
> **Best Practices**
>
> Remember, you don't have to use Trongate's form helper functions (like  form_button()) if you don't want to.  With Trongate MX, you can choose to work with the syntax that *you* like best.
> 
> 
> So, what will it be?  Form helpers or pure HTML?  The choice is yours!


