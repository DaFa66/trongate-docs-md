# Swap Operations


The `mx-swap` attribute determines how the response content is inserted into the target element, as specified by the `mx-target` attribute. If the `mx-swap` attribute is not provided, it defaults to `innerHTML`, which replaces the inner HTML of the target element.

## Available Swap Methods:


| Method | Description | Example Syntax |
| ---|---|---|
| innerHTML (default) | Replaces the inner HTML of the target element with the response content. | `mx-swap="innerHTML"` |
| outerHTML | Replaces the entire target element with the response content. | `mx-swap="outerHTML"` |
| textContent | Replaces the text content of the target element with the response content. | `mx-swap="textContent"` |
| beforebegin | Inserts the response content before the target element. | `mx-swap="beforebegin"` |
| afterbegin | Inserts the response content as the first child of the target element. | `mx-swap="afterbegin"` |
| beforeend | Inserts the response content as the last child of the target element. | `mx-swap="beforeend"` |
| afterend | Inserts the response content after the target element. | `mx-swap="afterend"` |
| delete | Removes the target element from the DOM. | `mx-swap="delete"` |
| value | Sets the value property of form elements (inputs, textareas, selects) with the response content. | `mx-swap="value"` |
| none | Does not insert any content into the DOM. Useful for out-of-band swaps where no direct DOM update is needed. | `mx-swap="none"` |

## Examples:

### Prepend Data:


This code sample below uses the `mx-swap="afterbegin"` method to insert the response content as the first child of the target element.


**PLEASE NOTE:**  This example uses Trongate's form_button() function.  There's no obligation to use Trongate's form helper functions and it's acceptable to work with pure HTML, if you wish.

```vf
<?php
$btn_attr = [
  'mx-get' =--> 'api/data',
  'mx-target' =&gt; '#task-list',
  'mx-swap' =&gt; 'afterbegin'
];
echo form_button('add_task_btn', 'Add New Task', $btn_attr);
?&gt;

<ul id="task-list">
  <li>Finish project documentation</li>
  <li>Review pull requests</li>
  <li>Update dependencies</li>
</ul>
```


Here's how you can accomplish the same using pure HTML:

```html
<button mx-get="api/data" 
        mx-target="#task-list" 
        mx-swap="afterbegin">Add New Task</button>

<ul id="task-list">
  <li>Finish project documentation</li>
  <li>Review pull requests</li>
  <li>Update dependencies</li>
</ul>
```


Clicking the button adds a new task to the top of the task list. For example, if the response text from the server is `<li>Schedule team meeting</li>`, it will become the first item in the list.


---

### Replace Entire Element:


Here, `mx-swap="outerHTML"` is used to replace the entire target element with the response content.


Using Trongate's form_button() function:

```vf
<?php
$btn_attr = [
  'mx-get' =--> 'api/data',
  'mx-target' =&gt; '#result',
  'mx-swap' =&gt; 'outerHTML'
];
echo form_button('replace_btn', 'Replace Element', $btn_attr);
?&gt;

<div id="result">Old Content</div>
```


For those who prefer working with pure HTML, the equivalent solution is here:

```html
<button mx-get="api/data" 
        mx-target="#result" 
        mx-swap="outerHTML">Replace Element</button>

<div id="result">Old Content</div>
```


---

### Insert Before Target:


This example demonstrates how to insert content before the target element using `mx-swap="beforebegin"`.


Using Trongate's form_button() form helper:

```vf
<?php
$btn_attr = [
  'mx-get' =--> 'api/data',
  'mx-target' =&gt; '#result',
  'mx-swap' =&gt; 'beforebegin'
];
echo form_button('insert_before_btn', 'Insert Before', $btn_attr);
?&gt;

<div id="result">Existing Content</div>
```


Alternatively, the same functionality can be achieved with pure HTML:

```html
<button mx-get="api/data" 
        mx-target="#result" 
        mx-swap="beforebegin">Insert Before</button>

<div id="result">Existing Content</div>
```


---

### Repopulate Form Field:


In the following example, `mx-swap="value"` is used to update the value of a form textarea element. This approach can be particularly useful for applications such as code beautifiers, date-pickers or any other tool that modifies form input values.


**PLEASE NOTE:** The code sample below utilises a variety of Trongate's form helper functions; however, their usage is entirely optional:

```vf
<?php 
$form_attr = [
   'mx-post' =--> 'beautify/submit_code',
   'mx-target' =&gt; '#code-input',
   'mx-swap' =&gt; 'value'
];
echo form_open('beautify/submit_code', $form_attr); 
echo form_textarea('my_code', '', array('id' =&gt; 'code-input'));
echo form_submit('submit', 'Beautify Code');
echo form_close();
?&gt;
```


If you prefer a more HTML-centered approach, you could use the following syntax:

```html
<form mx-post="beautify/submit_code" 
      mx-target="#code-input" 
      mx-swap="value">
  <textarea name="my_code" id="code-input"></textarea>
  <input type="submit" name="submit" value="Beautify Code">
</form>
```

> [!CAUTION]
> **Danger!**
>
> Building web applications with pure HTML forms could potentially expose your application to Cross-Site Request Forgery (CSRF) attacks. For more information, please refer to our documentation pertaining to [CSRF Protection](documentation/display/trongate_mx/trongate-mx-security/csrf-protection).


