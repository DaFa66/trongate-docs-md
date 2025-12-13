# Best Practices For Handling Data


Handling data securely is a cornerstone of building robust web applications. This page outlines best practices for managing user input, database interactions, and data rendering in the Trongate PHP framework, ensuring your application remains secure and efficient.

## Escaping Data: What and Why?


**Escaping data** is the process of converting potentially harmful characters into safe equivalents to prevent security vulnerabilities like Cross-Site Scripting (XSS). For example, converting `<` and `>` into `&lt;` and `&gt;` ensures that user input is treated as plain text, not executable code.

### Example of XSS Vulnerability


Consider a forum where a user posts:

```
<script>window.location.href="https://dangerous-website.com"</script>
```


Without escaping, this script would execute in users' browsers, redirecting them to a malicious site. Proper escaping ensures the input is rendered as harmless text.

## Common Misconceptions


A frequent mistake is escaping data **before inserting it into the database**. This corrupts the original data and limits its usability. Instead:


- **Store raw data** in the database.
- **Escape data at the point of rendering** to ensure it's safe for display.

## Risks of Improper Data Handling


Failing to handle data securely can lead to:


- **Cross-Site Scripting (XSS):** Malicious scripts executed in users' browsers.
- **SQL Injection:** Unauthorized database access or manipulation.
- **Data Corruption:** Loss of critical information due to premature escaping.

## Best Practices for Secure Data Handling

### 1. Validate Input


Ensure user input meets expected formats and values. Always validate on the server side, as client-side validation can be bypassed.

### 2. Sanitize Input


Remove unwanted characters (e.g., stripping HTML tags) to prevent injection attacks.

### 3. Escape at Rendering


Escape data when rendering it to the user, ensuring it's safe for the intended context (HTML, JavaScript, etc.).

### 4. Use Trongate's Model Class


The Trongate framework has a built-in [Model class](../../reference/class_reference/The_Model_Class) that has been designed for safe and effortless database interaction. If you use the Model class, you'll never have to worry about SQL injection attacks!


---

## How To Safely Display Submitted Data


Trongate provides the out() function to safely escape and format data for various output contexts. It ensures that user-submitted data can be displayed securely, preventing issues such as Cross-Site Scripting (XSS).


The `out()` function supports the following output formats:


- **HTML** (default)
- **XML**
- **JSON**
- **JavaScript**
- **HTML Attributes**

### When To Use out()


It's important to know when to use the `out()` function. Trongate's built-in helpers, such as form_input(), already handle escaping for you when generating form elements.  This means that there is no need to use `out()` when rendering form elements by usage of Trongate's  [form helper functions](../../reference/helpers/Form_Helpers).  However, in other contexts, you should use the `out()` function, especially when manually outputting user-submitted data. Examples include:


- Displaying dynamic content directly in an HTML document
- Inserting user-submitted data into JavaScript, JSON, or XML
- Escaping data for use in custom HTML attributes

### Example Usage:


Here's how you can use the out() function to escape user-submitted data for safe inclusion in an HTML context:

```php
$user_input = '<script>alert("XSS");</script>';
echo out($user_input); // Outputs: &lt;script&gt;alert(&quot;XSS&quot;);&lt;/script&gt;
```

### Other Output Formats:


You can specify the desired output format using the third parameter:

#### JSON:

```php
$user_input = '<div>example</div>';
echo out($user_input, 'UTF-8', 'json'); // Outputs: "\u003Cdiv\u003Eexample\u003C\/div\u003E"
```

#### JavaScript:

```php
$user_input = "Hello 'world'";
echo out($user_input, 'UTF-8', 'javascript'); // Outputs: "Hello \u0027world\u0027"
```

### Best Practices:


- For dynamic content outside of form_helpers (e.g., displaying raw user input in HTML, JSON, or JavaScript), use the out() function to ensure proper escaping.
- When using Trongate's **form_helpers**, such as form_input(), you don't need to use out() for attributes, as escaping is already handled internally.
- Specify the appropriate output format for the context where the data will be used (e.g., JSON, JavaScript).


By using the out() function appropriately and relying on Trongate's built-in helpers where applicable, you can ensure your application remains secure while following best practices.


---

## Database Interaction with Trongate's Model Class


Trongate's `Model` class simplifies secure database interactions. Use it to insert, update, and query data without compromising security.

### Example: Inserting or Updating Records

```php
public function submit(): void {
    $this->module('trongate_security');
    $this->trongate_security->_make_sure_allowed();

    $data = $this->get_data_from_post();
    $update_id = segment(3, 'int');

    if ($update_id > 0) {
        $this->model->update($update_id, $data, 'tasks');
        set_flashdata('Record updated successfully');
    } else {
        $this->model->insert($data, 'tasks');
        set_flashdata('Record created successfully');
    }

    redirect('tasks/show/' . $update_id);
}
```

> [!NOTE]
> **Just To Let You Know...**
>
> Full documentation regarding Trongate's Model class is offered in the [Database Operations](../0088Database_operations) chapter.
> 
> 
> In addition, all of the methods available within Trongate's Model class are detailed in the [API Reference Guide](../../reference/class_reference/The_Model_Class).


## In Summary


By following these best practices, you can ensure your Trongate application handles data securely and efficiently:


- **Validate and sanitize** user input.
- **Escape data at the point of rendering** using the `out()` function.
- **Interact with the database securely** using Trongate's `Model` class.


Adhering to these principles will help to keep your applications both robust and secure.

