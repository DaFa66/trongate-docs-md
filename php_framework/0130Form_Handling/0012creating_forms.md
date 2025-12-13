# Creating Forms


Trongate contains a wide assortment of in-built [form helpers](../../reference/helpers/Form_Helpers) to assist with form building. Form helpers are a set of PHP functions designed to simplify the process of creating and managing HTML forms within your application.


With Trongate, all form helpers are available immediately and with no requirement to load anything. There is also no need to update any configuration files if you want to use Trongate's form helpers. In short, they just work "out of the box".

> [!NOTE]
> **Just To Let You Know...**
>
> A comprehensive list of Trongate's form helper functions is available from the [Trongate API Guide](../../reference/helpers/Form_Helpers).


## Opening A Form


The creation of an HTML form that posts data to an endpoint (URL) requires a form opening tag. A form opening tag typically contains:


1. A method property
2. A form location


In normal (vanilla) HTML, this could be written like so:

```html
<form action="tasks/submit" method="post">
```

> [!NOTE]
> **Just To Let You Know...**
>
> The above form opening tag has an **action** property with a value of 'tasks/submit'. This means that the form is going to submit an HTTP request to the URL `tasks/submit`.
> 
> 
> The form opening tag (above) also has a **method** property with an assigned value of 'post'. This means that submission of the form will result in an HTTP **POST** request being made.


### Trongate's Form Open Function


With Trongate's form_open() function, an opening form tag can easily be rendered from within a view file.  For example:

```vf
echo form_open('tasks/submit');
```


Having this code inside a view file will result in the following HTML being rendered:

```html
<form action="tasks/submit" method="post">
```

> [!TIP]
> **Best Practices**
>
> When using Trongate's form_open() function, it's a good practice to declare the form location from within a controller file and to then have the form location passed into the corresponding view file. For example:
> 
> ```php
> function create() {
>   $data['form_location'] = 'tasks/submit';
>   $this->view('form', $data);
> }
> ```
> 
> 
> When Trongate's view() method is invoked, the second argument (i.e., the `$data` array) is automatically extracted, making the following syntax possible:
> 
> ```vf
> echo form_open($form_location);
> ```


> [!WARNING]
> Don't forget to use opening and closing PHP tags when adding PHP to a view file!  For example:
> 
> ```vf
> <h1>Create New Task</h1>
> <?php
> echo form_open($form_location);
> // rest of the form to go here...
> ?>
> ```



---

## Rendering Form Elements


Having produced a form opening tag, your next goal should be to render form elements such as form input fields. A full breakdown of all available form elements can be viewed [here](../../reference/helpers/Form_Helpers). In the meantime, and for brevity, here are some commonly used form helpers that can be used to generate form elements.

### Input Fields


The form_input() helper function can be used to create an HTML form input element, for text input. For example:

```php
echo form_input('username', 'John');
```


In the code sample above, the first parameter represents the 'name' attribute, and the second is the default value. This means that the above code snippet would render a form input field that has been pre-populated with the username, 'John'.


The PHP code above would render the following HTML:

```html
<input type="text" name="username" value="John">
```

> [!TIP]
> **Best Practices**
>
> Form helpers automatically handle proper escaping. Therefore, do not combine form helpers with the out() function or manual escaping functions.


### Textareas


The form_textarea() function mirrors `form_input()` in every way except that it creates a "textarea" element.

```php
echo form_textarea('description', '');
```


In the code sample above, the first parameter represents the 'name' attribute, and the second is the default value for the textarea. In the code snippet above, the default value has been set to an empty string. This would produce an empty textarea element, like so:

```html
<textarea name="description"></textarea>
```

### Dropdowns


The form_dropdown() helper function generates an HTML select (dropdown) element with multiple options. For example:

```php
$options = array(
  'small'  => 'Small Shirt',
  'med'    => 'Medium Shirt',
  'large'  => 'Large Shirt',
  'xlarge' => 'Extra Large Shirt',
);
echo form_dropdown('size', $options, 'large');
```


In the example above, the first parameter represents the 'name' attribute, the second is an associative array of options, and the third is the selected option.


Here's the HTML that would be rendered by the above code sample:

```html
<select name="size">
    <option value="small">Small Shirt</option>
    <option value="med">Medium Shirt</option>
    <option value="large" selected="selected">Large Shirt</option>
    <option value="xlarge">Extra Large Shirt</option>
</select>
```

### Checkboxes and Radio Buttons


The form_checkbox() and form_radio() helper functions are used to create checkbox and radio button elements, respectively. For example:

```php
echo form_checkbox('newsletter', 'accept', true);
echo form_radio('gender', 'male', true);
```


In the code above, the first parameter represents the 'name' attribute, the second is the value, and the third is a boolean indicating whether the element should be checked by default.


Here's the HTML code that would be produced from the form_checkbox() code snippet, as shown above:

```html
<input type="checkbox" name="newsletter" value="accept" checked="checked">
```


Here's the HTML code that would be produced from the form_radio() code snippet, as shown above:

```html
<input type="radio" name="gender" value="male" checked="checked">
```

### File Input


The form_file_select() helper function generates an HTML file input element for file uploads. For example:

```php
echo form_file_select('file_upload');
```


In this example, the first parameter represents the 'name' attribute of the file input element.


Here's the HTML code that would be produced from the above code snippet:

```html
<input type="file" name="file_upload">
```

### Submit Button


The form_submit() helper function creates an HTML submit button for submitting forms. For example:

```php
echo form_submit('submit', 'Submit Form');
```


In the example above, the first parameter represents the 'name' attribute, and the second is the button's label text.


Here's the HTML code that would be produced from the above code snippet:

```html
<button type="submit" name="submit">Submit Form</button>
```


---

## Closing the Form


The form_close() helper function is used to close an open form. It not only generates the closing form tag but also includes a hidden CSRF token field for enhanced security. For example:

```php
echo form_close();
```


Here's the HTML code that would be produced from the above code snippet:

```html
<input type="hidden" name="csrf_token" value="[random_token]">
</form>
```


Note: The `[random_token]` placeholder represents a dynamically generated CSRF token value for security purposes.

> [!TIP]
> **Best Practices**
>
> Trongate's inbuilt CSRF protection is activated when:
> 
> 
> 1. The form_close() function has been used to render a form close tag
> 2. The run(), within Trongate's [Validation class](../../reference/class_reference/The_Validation_Class) has has been invoked
> 
> 
> Always use form_close(), and validate submitted form fields using the run() method from Trongate's [Validation](../../reference/class_reference/The_Validation_Class) class, to ensure proper form closure and CSRF protection. This is especially important for forms that handle sensitive data.


> [!NOTE]
> **Just To Let You Know...**
>
> A full explanation of how Trongate's in-built CSRF protection works - under the hood - can be found in the [Trongate MX Guide](../../trongate_mx/0076Trongate_MX_Security/0079csrf_protection.md).



---

## Form Attributes


Most of Trongate's form helper functions can accept an array of attributes to customize form elements:

```vf
$attributes = array('class' => 'sm', 'style' => 'width:50%');
echo form_input('username', 'Your Username', $attributes);
```


This will generate an input field with the specified class and style attributes.

```html
<input type="text" name="username" value="Your Username" class="sm" style="width:50%">
```

> [!NOTE]
> **Just To Let You Know...**
>
> In PHP, there are several different types of syntax that can be used to initialize arrays.  The following examples produce precisely the same output though with very different (though perfectly valid) PHP syntax:
> 
> 
> **Example 1**
> 
> ```php
> $attr['class'] = 'sm';
> $attr['placeholder'] = 'Enter username here...';
> $attr['autocomplete'] = 'off';
> echo form_input('username', '', $attr);
> ```
> 
> 
> **Example 2**
> 
> ```php
> $attr = [
>   'class' => 'sm',
>   'placeholder' => 'Enter username here...',
>   'autocomplete' => 'off'
> ];
> echo form_input('username', '', $attr);
> ```
> 
> 
> **Example 3**
> 
> ```php
> $attr = array('class' => 'sm', 'placeholder' => 'Enter username here...', 'autocomplete' => 'off');
> echo form_input('username', '', $attr);
> ```
> 
> 
> **Defining Attributes Within Helpers**
> 
> 
> For brevity, you can also define an array of attributes from *within* a form helper function.  For example,
> 
> ```php
> echo form_input('username', '', array('class' => 'sm'));
> ```
> 
> 
> All of the different types of coding styles shown above are valid.



---

## Complete Form Example


Below is a complete example of how to create a form in Trongate. This example includes a controller method and a corresponding view file.

### Controller Method


The controller method initializes the form data and passes it to the view file:

```php
public function create(): void {
    $data['headline'] = 'Create New Task';
    $data['form_location'] = BASE_URL.'tasks/submit';
    $data['cancel_url'] = BASE_URL.'tasks/manage';
    $data['task_title'] = ''; // Default value for task title
    $data['task_description'] = ''; // Default value for task description
    $data['complete'] = false; // Default value for checkbox

    $this->view('tasks/create', $data);
}
```

### View File


The view file contains the HTML and PHP code to render the form:

```vf
<h1><?= $headline ?></h1>
<div class="card">
    <div class="card-heading">
        Task Details
    </div>
    <div class="card-body">
        <?php
        echo form_open($form_location);
        echo form_label('Task Title');
        echo form_input('task_title', $task_title, array("placeholder" => "Enter Task Title"));
        echo form_label('Task Description');
        echo form_textarea('task_description', $task_description, array("placeholder" => "Enter Task Description"));
        echo '<div>';
        echo form_label('Complete');
        echo form_checkbox('complete', 1, $complete);
        echo '</div>';
        echo form_submit('submit', 'Submit');
        echo anchor($cancel_url, 'Cancel', array('class' => 'button alt'));
        echo form_close();
        ?>
    </div>
</div>
```


This example demonstrates how to create a form for adding a new task. The form includes fields for the task title, description, and a checkbox to mark the task as complete. The form also includes a submit button and a cancel link.


---

## The Benefits of Using Trongate's Form Helpers


Trongate's form helper functions offer several advantages over raw HTML:


- **Automatic Security:** Values are escaped using HTML entity encoding to prevent XSS vulnerabilities.
- **Validation Integration:** Seamless error highlighting and repopulation after form validation failures.
- **CSRF Protection:** Built-in CSRF token generation through the `form_close()` function.
- **Consistent Syntax:** PHP-based helpers reduce context switching between HTML and PHP.
- **Reduced Boilerplate:** Simplified creation of complex elements like dropdowns and checkboxes.

Example using form helper:

```php
<?= form_input('username', post('username')) ?>
```


Equivalent raw HTML:

```html
<input type="text" name="username" value="<?= htmlspecialchars($_POST['username'] ?? '', ENT_QUOTES) ?>">
```
