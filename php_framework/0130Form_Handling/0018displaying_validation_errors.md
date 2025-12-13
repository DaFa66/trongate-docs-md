# Displaying Validation Errors


When a form is submitted and validation errors are produced, it is standard practice to re-present the form to users. It's also standard practice to present users with form validation errors in those instances. This approach gives users an opportunity to correct their input without losing the information they have already entered.


The typical technique for re-presenting forms to end users is to invoke the method responsible for displaying the previous page (i.e., the page that renders the HTML form). For example:

```php
$result = $this->validation->run();

if ($result === true) {
    echo 'Form submission successful!';
} else {
    // Form submission error (re-present the form to the user)
    $this->create();
}
```


By immediately re-invoking the **`create()`** method, as shown above, the entire page that renders the HTML form will be re-rendered.

> [!NOTE]
> **Just To Let You Know...**
>
> The example above assumes that there is a `create()` method within the containing controller file. When invoked, this `create()` method would render a webpage that contains the form to be filled out and submitted.
> 
> 
> Of course, there's no obligation to name the method 'create'. Here's a very basic example of a method that could be added to a controller file with the purpose of rendering a 'contact us' form:
> 
> ```php
> function contact() {
>     $data['first_name'] = post('first_name', true);
>     $data['last_name'] = post('last_name', true);
>     $data['email_address'] = post('email_address', true);
>     $data['view_file'] = 'contact_form';
>     $this->template('public', $data);
> }
> ```
> 
> 
> As you can see, *not only* is the method declaring a view file name ('contact_form') and loading a template, it's *also* retrieving submitted form data and passing it into the view file. This means that the form being rendered will be prepopulated with previously submitted values. The code for a form that is rendered by the `contact()` method shown above could look like this:
> 
> ```vf
> <?php
> echo form_open('your_submit_url');
> 
> echo form_label('First Name');
> echo form_input('first_name', $first_name, array("placeholder" => "Enter First Name"));
> 
> echo form_label('Last Name');
> echo form_input('last_name', $last_name, array("placeholder" => "Enter Last Name"));
> 
> echo form_label('Email Address');
> echo form_input('email_address', $email_address, array("placeholder" => "Enter Email Address"));
> 
> echo form_submit('submit', 'Submit');
> echo form_close();
> ?>
> ```



When forms that produce validation errors are re-presented to the end user, an array of form validation errors will be made available.


There are two techniques that can be used to display validation errors:


1. Traditional
2. Inline

## 1. Traditional Validation Errors Display


This approach involves displaying all validation errors at once, typically at the top of the form.

![normal form validation errors](https://trongate.io/images/validation_errors_normal.png)
        
*A screenshot depicting form validation errors being presented as a block of text.*
### How to Implement:


- Use the run() method to execute form validation checks.
- If the `run()` method returns a value of **true** (boolean), you may assume that the submitted form field values have **passed** all of the form validation checks.
- On the other hand, if the `run()` method returns a value of **false** (boolean), this means that one or more form validation errors have been produced.

```php
$result = $this->validation->run();

if ($result === true) {
    echo 'Form submission successfully passed all validation tests!';
} else {
    // Form submission error(s) were produced
    $this->create(); // re-present the form to the end user
}
```
In your view file, use the validation_errors() function to display all validation errors. The code below demonstrates how to render validation errors using PHP short tags:```vf
<?= validation_errors() ?>
```

The validation_errors() method will display all of the form validation errors together. The line of code responsible for rendering the validation errors is usually placed inside a view file and above the corresponding form.

> [!NOTE]
> **Just To Let You Know...**
>
> By default, the validation_errors() function renders error messages as red text within `<p>` tags. However, Trongate offers flexibility in customizing the appearance of these error messages:
> 
> 
> 1. **Custom HTML wrapping:** You can pass optional arguments to `validation_errors()` to control the HTML wrapping of individual error messages. For example:
> 2. **Global configuration:** For site-wide customization, you can define the PHP constants `ERROR_OPEN` and `ERROR_CLOSE` in your `config.php` file. When set, these constants will be used as the default HTML wrapping for **all** validation errors. For example:
> 
> 
> These options allow you to easily integrate validation error displays with your site's design and CSS, ensuring a consistent look and feel across your application.


## 2. Inline Validation Errors Display


Trongate offers an alternative methodology for displaying form validation errors: **inline validation errors**.


With *inline validation errors* applied, individual form validation errors are displayed next to their respective form fields, providing what some consider to be a more modern user experience.

![inline form validation errors](https://trongate.io/images/validation_errors_inline.png)
        
*A screenshot depicting inline form validation errors.*
### How to Implement:


1. Add the class `highlight-errors` to your form tag.
2. For each form field, use the validation_errors() function with the field name as an argument.


For example:

```vf
echo form_open($form_location, array('class' => 'highlight-errors'));

echo form_label('Username');
echo validation_errors('username');
echo form_input('username', $username, array("placeholder" => "Enter Username"));

echo form_label('First Name');
echo validation_errors('first_name');
echo form_input('first_name', $first_name, array("placeholder" => "Enter First Name"));

echo form_label('Last Name');
echo validation_errors('last_name');
echo form_input('last_name', $last_name, array("placeholder" => "Enter Last Name"));

echo form_label('Email Address');
echo validation_errors('email_address');
echo form_input('email_address', $email_address, array("placeholder" => "Enter Email Address"));

echo form_submit('submit', 'Submit');
echo anchor($cancel_url, 'Cancel', array('class' => 'button alt'));
echo form_close();
```


This method will display errors inline, next to their respective fields.

> [!TIP]
> **Best Practices**
>
> In situations where inline form validation errors appear, an alert will appear at the top of the page that:
> 
> 
> 1. Makes the user aware that something went wrong.
> 2. Informs the user that more details are 'highlighted below'.
> 
> 
> This alert is contained within a CSS class named **`.validation-error-alert`**. If you do not wish the alert to appear, simply apply a CSS rule to the page that forces the element to remain hidden. For example:
> 
> ```css
> .validation-error-alert {
>     display: none;
> }
> ```



By effectively utilizing these validation error display techniques, you can create user-friendly forms that provide clear feedback, improving the overall user experience of your Trongate application.

> [!NOTE]
> **Just To Let You Know...**
>
> For those aiming to give users an even better experience, please check out [Trongate MX](../../trongate_mx) - Trongate's new front-end framework. Trongate MX gives Trongate developers the ability  to build extremely sophisticated and fully interactive forms, **without writing any JavaScript**. All of this is covered in the [Form Handling](../../trongate_mx/0065Form_Handling) chapter.


