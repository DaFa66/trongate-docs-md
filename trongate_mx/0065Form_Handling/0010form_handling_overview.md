# Form Handling Overview


Building modern web applications requires forms that are both powerful and user-friendly. Trongate MX transforms traditional form handling into a seamless experience, eliminating page reloads while maintaining the robust security you expect from the Trongate PHP framework.

## Understanding the Evolution


Traditional form handling follows a predictable pattern: users fill out forms, submit data through POST requests, and servers respond with either validation errors or success redirects. While reliable, this approach often creates a jarring experience as pages reload and users wait for responses.


Trongate MX retains this trusted foundation while adding powerful dynamic capabilities:


- Forms submit asynchronously, eliminating disruptive page reloads.
- Real-time validation provides instant feedback to users.
- Success and error states display smoothly with built-in animations.
- Forms can update, hide, or transform based on user interactions.

## The Power of MX Attributes


At the heart of Trongate MX's form handling are special `mx-` attributes. These declarative HTML attributes unlock dynamic functionality without requiring JavaScript knowledge. For example:

```vf
<?php
$form_attr = [
  'mx-post' => 'users/create',
  'mx-target' => '#response'
];
echo form_open('#', $form_attr);
// Form fields go here.
echo form_submit('submit', 'Submit');
echo form_close();
?>

<div id="response"></div>
```


This simple markup creates a form that:


- Submits data asynchronously to the 'users/create' endpoint.
- Updates a specific page element when the submission completes.

> [!NOTE]
> **Just To Let You Know...**
>
> The view file code (displayed above) renders the following HTML:
> 
> ```html
> <form mx-post="users/create" mx-target="#response" action="#" method="post">
>   <button type="submit" name="submit">Submit</button>
> </form>
> 
> <div id="response"></div>
> ```
> 
> 
> The `mx-post` attribute ensures the form's behaviour is both dynamic and intuitive.


## About Form Opening Tags


In Trongate MX, if `mx-post` is used alongside `action` and `method` properties (within a form opening tag), the `mx-post` attribute takes precedence.


To learn more about the `mx-post` attribute, [click here](documentation/display/trongate_mx/core-http-operations/http-methods-in-trongate-mx).

## An Enhancement, Not a Replacement


Trongate MX enhances rather than replaces traditional form handling. All security features from the Trongate PHP framework remain fully functional. All of Trongate's helper functions continue to work, the validation class operates seamlessly, server-side validation remains robust, CSRF protection is automatic, and you can freely mix traditional and enhanced form handling approaches within the same application.


In the following sections, we'll explore how to implement these features in your own applications, starting with the basics of form construction and moving on to advanced interaction patterns.

