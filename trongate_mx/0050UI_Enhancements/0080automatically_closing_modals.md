# Automatically Closing Modals


Trongate MX has two attributes for closing dynamic modals: `mx-close-on-success` and `mx-close-on-error`. These attributes work in conjunction with dynamically created modals to provide enhanced modal control.

## Demonstration


Click on the 'Create Modal' button to see a demonstration of automatic modal closing.

Create Modal
## Basic Modal Creation and Closure


Let's start by creating a module that we can use for testing purposes.


We'll call the module '**test**' and the URL for displaying your basic 'Create Modal' button will be:

```
<base-url>test/demo1
```

> [!NOTE]
> **Just To Let You Know...**
>
> The `<base-url>` string is a placeholder for your website's base URL.



The controller file for your 'test' module should be named as '**Test.php**'.  In addition, the name of the method that will be used for rendering your test page will be '**demo1**'. Here's the starter code for the 'Test.php' controller file:

```php
<?php
class Test extends Trongate {

    function demo1() {
        $data['view_file'] = 'demo1';
        $this->template('public', $data);
    }

}
```


And here's the corresponding view file (demo1.php):

```vf
<h1 class="text-center">Basic Modal Creation and Closure</h1>
<p class="text-center">Click on the 'Create Modal' button.</p>
<p class="text-center">
    <?php
    // Define the button attributes
    $btn_attr = [
        'mx-get' => 'test/simple_modal_content',
        'mx-build-modal' => 'demo-modal'
    ];

    // Create the button using Trongate's form_button function
    echo form_button('create_modal_btn', 'Create Modal', $btn_attr);
    ?>
</p>
```


Here's a pure HTML example that accomplishes the same goal:

```html
<h1 class="text-center">Basic Modal Creation and Closure</h1>
<p class="text-center">Click on the 'Create Modal' button.</p>
<p class="text-center">
    <button mx-get="test/simple_modal_content"
            mx-build-modal="demo-modal">Create Modal</button>
</p>
```

### Setting Up the Modal Content Endpoint


Now, let's create an endpoint that serves the modal content.  This endpoint should return the HTML for your modal body.  For this example, let's create a method named '**simple_modal_content**'.  Below is the code for this method and please *do* add this to your 'Test.php' controller file:

```php
// This method returns the HTML content that will populate the modal
function simple_modal_content() {
    $data['form_location'] = 'test/simulate_form_success';

    // Load a view containing your form
    $this->view('simple_modal_content', $data);
}
```


Here's the corresponding view file content (simple_modal_content.php):

```vf
<p>Click the 'Submit' button to simulate a successful form submission.</p>
<?php
$form_attr = [
    'mx-post' => $form_location,
    'mx-close-on-success' => 'true'
];
echo form_open('#', $form_attr);
echo form_submit('submit', 'Submit');
echo form_close();
```


If you'd rather **not** using Trongate's form helper functions, here's an alternative syntax that could be used:

```vf
<p>Click the 'Submit' button to simulate a successful form submission.</p>
<form mx-post="<?= $form_location; ?>" mx-close-on-success="true">
    <button type="submit" name="submit">Submit</button>
</form>
```

> [!CAUTION]
> **Danger!**
>
> Building applications with pure HTML forms can create potential security risks. See our [CSRF Protection](CSRF Protection) documentation for details.


> [!NOTE]
> **Just To Let You Know...**
>
> There are no form fields in the code above since the goal is to produce the most basic example possible.  After the 'Submit' button is pressed, the goal is to return a 'success' response from the API, regardless of what has been posted to the endpoint.


### Handling Form Submission


The endpoint that handles the form submission is going to be really simple.  It will return an HTTP response status code of 200, indicating form submission success.


Our endpoint will be served via a method named as '**simulate_form_success**'.

```php
function simulate_form_success() {
    http_response_code(200);
}
```

### Complete Controller File Code


If you've been following along, your controller file - for this first demonstration - should be as follows:

```php
<?php
class Test extends Trongate {

    function demo1() {
        $data['view_file'] = 'demo1';
        $this->template('public', $data);
    }

    // This method returns the HTML content that will populate the modal
    function simple_modal_content() {
        $data['form_location'] = 'test/simulate_form_success';
        
        // Load a view containing your form
        $this->view('simple_modal_content', $data);
    }

    function simulate_form_success() {
        http_response_code(200);
    }

}
```

## Adding Visual Feedback


For a better user experience, we can add animations to provide visual feedback.  This can be achieved by adding the `mx-animate-success` attribute to the form and giving it a value of 'true':

```vf
<p>Click the 'Submit' button to simulate a successful form submission.</p>
<?php
$form_attr = [
    'mx-post' => $form_location,
    'mx-close-on-success' => 'true',
    'mx-animate-success' => 'true'
];
echo form_open('#', $form_attr);
echo form_submit('submit', 'Submit');
echo form_close();
```


For an alternative HTML-centered approach, here's the corresponding code:

```vf
<p>Click the 'Submit' button to simulate a successful form submission.</p>
<form mx-post="<?= $form_location; ?>" 
      mx-close-on-success="true" 
      mx-animate-success="true">
    <button type="submit" name="submit">Submit</button>
</form>
```

> [!NOTE]
> **Just To Let You Know...**
>
> This page covers how to **automatically** close modal windows after an HTTP request has been executed using Trongate MX.
> 
> 
> Whilst this feature may be useful (and we hope it is!), don't forget that you can make manual closing of modal elements possible by usage of the JavaScript function `closeModal()`.
> 
> 
> Below is an example of a simple button that - when clicked - will close any modal windows that are currently visible:
> 
> ```html
> <button onclick="closeModal()">Close Window</button>
> ```


## Handling Error Responses


While the previous example demonstrated closing modals on successful API responses, Trongate MX also supports automatic modal closure when receiving error responses (HTTP status codes outside 200-299).


To implement this, modify two key attributes in your form:

```vf
<p>Click the 'Submit' button to simulate an error response.</p>
<?php
$form_attr = [
    'mx-post' => $form_location,
    'mx-close-on-error' => 'true',
    'mx-animate-error' => 'true'
];
echo form_open('#', $form_attr);
echo form_submit('submit', 'Submit');
echo form_close();
?>
```


Here's an alternative syntax for developers who prefer to work with pure HTML:

```vf
<p>Click the 'Submit' button to simulate an error response.</p>
<form mx-post="<?= $form_location; ?>" 
        mx-close-on-error="true" 
        mx-animate-error="true">
    <button type="submit" name="submit">Submit</button>
</form>
```

> [!NOTE]
> **Just To Let You Know...**
>
> For this to work, your API endpoint should return an appropriate **error** status code.  For example:
> 
> ```php
> function simulate_form_error() {
>     http_response_code(400);
> }
> ```



The key changes from the success example are the introduction of; `mx-close-on-error="true"` (which triggers modal closure when receiving error responses) and `mx-animate-error="true"` (which displays a red cross animation before the modal closes).

> [!NOTE]
> **Just To Let You Know...**
>
> When the form submission results in an error response, Trongate MX will draw a red cross animation before closing the modal.


## Summary


Trongate MX provides two specialized 'mx' attributes for automatic closing of modal elements:


- `mx-close-on-success`
- `mx-close-on-error`


These can be enhanced with animation attributes that render 'success' or 'error' animations immediately before modal closure:


- `mx-animate-success`
- `mx-animate-error`


These attributes, alongside other Trongate MX features, can be combined to create highly responsive, interactive user interfaces while minimizing JavaScript dependencies.


Don't forget, you can also add `onclick="closeModal()"` to elements, like buttons, to have modal windows close with user interaction such as clicks.

