# Identifying Trongate MX Requests


When working with Trongate MX, it's often useful to know whether a request originated from Trongate MX or from another source. Trongate's PHP framework includes a function called from_trongate_mx() in its engine directory that helps identify these requests.

> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** The from_trongate_mx() function resides in Trongate's engine directory and is part of the PHP framework. While Trongate MX automatically sets the required header, the detection happens on the server side using this PHP function.


## How It Works


Trongate MX automatically adds a special header (`Trongate-MX-Request: true`) to all requests it makes. The from_trongate_mx() function checks for the presence of this header.


| Scenario | Description | Result |
| ---|---|---|
| Trongate MX Request | Request made using mx-get, mx-post, etc. | from_trongate_mx() returns `true` |
| Regular HTTP Request | Standard form submission, AJAX, etc. | from_trongate_mx() returns `false` |
| Page Load | Direct URL visit or page refresh | from_trongate_mx() returns `false` |

> [!NOTE]
> **Just To Let You Know...**
>
> The code examples below use `if (from_trongate_mx() === true)` for explicit boolean checks.  However, the simpler syntax `if (from_trongate_mx())` will also work. Both approaches are valid, and you can choose the one that best suits your coding style or project requirements.


## Common Use Cases

### 1. Differentiating Response Formats


The code sample below demonstrates a method (i.e., a function within a class) that could serve as an API endpoint for an HTTP request.  In the example, we're using from_trongate_mx() to determined if the inbound HTTP request was submitted using Trongate MX.

```php
public function get_users() {

    $users = $this->model->get('users');
    
    if (from_trongate_mx() === true) {
        // Return HTML for dynamic update
        $data['users'] = $users;
        $html = $this->view('users_list', $data);
        echo $html;
    } else {
        // Return full page for direct visits
        $data['users'] = $users;
        $data['view_module'] = 'users';
        $data['view_file'] = 'users_page';
        $this->template('admin', $data);
    }

}
```

### 2. Handling Form Submissions


This next example demonstrates a method handles form submissions differently depending on the context of the request. Specifically, it uses from_trongate_mx() to determine if the form submission originated from a Trongate MX request or a traditional form submission.

```php
public function submit_form() {

    $name = post('name', true);
    
    if (from_trongate_mx() === true) {
        // Return targeted update
        echo "<div class='alert success'>Thanks, $name!</div>";
    } else {
        // Redirect for traditional form submit
        redirect('thank_you_page');
    }

}
```


In the code example above, if the request is found to have originated from Trongate MX:


- A 'thank you' message is rendered.


If the request is found to have **not** originated from Trongate MX:


- The end user will be redirected to a different URL.

> [!NOTE]
> **Just To Let You Know...**
>
> In the example above, we haven't actually *processed* any form data!  So, please *do* keep in mind the fact that some of these examples have been deliberately simplified.  In a real-world application, you'd probably have a requirement to *do something* with submitted form data.


### 3. API Response Formatting


The final example shows how to adjust API responses based on the request type. If the request comes from Trongate MX, the method returns HTML for seamless frontend updates. For other requests, it outputs JSON, making the endpoint suitable for *both* Trongate MX usage *as well as* more traditional API use.

```php
public function get_data() {

    $data = $this->model->get('items');
    
    if (from_trongate_mx() === true) {
        // Return HTML for dynamic insertion
        $html = $this->view('items_list', ['items' => $data]);
        echo $html;
    } else {
        // Return JSON for API consumers
        echo json_encode($data);
    }
    
}
```

> [!TIP]
> **Best Practices**
>
> - Use from_trongate_mx() when you need different response formats for dynamic updates versus direct visits
> - Consider using it for form submissions where you want different success behaviors
> - Leverage it to provide appropriate error responses based on the request source
> - Remember that the function is part of Trongate's PHP framework, not Trongate MX itself


## Summary


Being able to identify Trongate MX requests enables you to create endpoints that can serve both dynamic updates and traditional page loads effectively. The from_trongate_mx() function provides a simple way to detect these requests and adjust your response accordingly, making it easier to build applications that work seamlessly with both Trongate MX and traditional HTTP requests.

