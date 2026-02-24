# Other Helpful Features


Trongate includes several useful features that are not part of any specific helper file or class but play an integral role in streamlining web development. These features can be accessed from within any module controller or view file.

## The Anchor Function


The anchor() function generates a clickable text link pointing to a URL relative to `BASE_URL`.


For instance, if the website *example.com* has a homepage located at:

```
https://example.com
```


A contact page at `https://example.com/contact` can be linked using:

```vf
<?= anchor("contact", "Get In Touch") ?>
```


This function accepts up to three parameters:


- **$target_url** ~ The destination URL.
- **$text** ~ The displayed link text.
- **$attributes** (optional) ~ An array of key-value pairs added to the opening 'a' tag.


This function supports both internal and external links by providing a full URL as an argument.

> [!CAUTION]
> **Security Note:** The anchor() function does **not** escape the link text. For user-generated or database content, consider combining with the out() function to prevent XSS attacks:
> 
> ```vf
> <?= anchor("contact", out($user_provided_text)) ?>
> ```


> [!TIP]
> **Best Practices**
>
> When using HTML in links (such as Font Awesome icons), make sure the content is from a trusted source:
> 
> ```vf
> <?= anchor("home", 'Home <i class="fa fa-home"></i>') ?>
> ```
> 
> 
> For user-generated content, use in combination with the out() function.  For example:
> 
> ```vf
> <?= anchor("user-profile", out($username)) ?>
> ```


## The IP Address Function


The ip_address() function returns the IP address of the current visitor. Syntax:

```php
ip_address();
```


Example usage in a view file:

```php
// Inside a view file
Your IP Address is <?= ip_address() ?>.
```

## Generating Random Strings


The make_rand_str() function generates random strings. Example:

```php
$str = make_rand_str(32);
```


The first argument specifies the string length. Passing **true** as a second argument ensures uppercase output:

```php
$code = make_rand_str(6, true);
echo $code; // Example output: "A4WX28"
```

> [!NOTE]
> **Just To Let You Know...**
>
> Characters prone to misinterpretation (e.g., '0', '1', 'l') are excluded for clarity, particularly in scenarios where users read codes aloud.


## APPPATH


The `APPPATH` constant returns the absolute file path of the application directory. Example:

```php
echo APPPATH;
```


Within a view file, the `APPPATH` can be rendered using PHP short tags, like so:

```vf
<?= APPPATH ?>
```

> [!NOTE]
> **Just To Let You Know...**
>
> The `BASE_URL` constant is also available, returning the main website URL as defined in `config.php`:
> 
> ```php
> echo BASE_URL;
> ```


## The JSON Function


The json() function provides a visual representation of data within controllers or views. Syntax:

```php
json($data);
```


The optional second argument, when set to **true**, terminates script execution after displaying the data.


Example usage in a view file:

```vf
<h1><?= $headline ?><span class="sm">(Record ID: <?= $update_id ?>)</span></h1>
<?= json($data) ?>
<div class="card">
  <div class="card-heading">
    Options
  </div>
  <div class="card-body">
    <?php
    echo anchor('members/manage', 'View All Members', array("class" => "button alt"));
    echo anchor('members/create/'.$update_id, 'Update Details', array("class" => "button"));
    $attr_delete = array(
      "class" => "danger go-right",
      "id" => "btn-delete-modal",
      "onclick" => "openModal('delete-modal')"
    );
    echo form_button('delete', 'Delete', $attr_delete);
    ?>
  </div>
</div>
```


Sample output:



    ![screenshot](https://dafadev.net/a1/images/35/json_scrfqQY.png)
    
*Screenshot showing sample output after having invoked the `json()` function.*


## The Out Function


The out() function escapes and formats strings for safe output in different contexts. Parameters:


- **$input** ~ The string to escape.
- **$encoding** (optional) ~ Character encoding (default: 'UTF-8').
- **$output_format** (optional) ~ Output format: 'html' (default), 'xml', 'json', 'javascript', or 'attribute'.

### Example 1: Safe Output from JSON Data

```php
$jsonString = "{"name": "<script>alert(\"XSS Attack\");</script>", "age": 25}";
$data = json_decode($jsonString, true);

echo "<p>Name: ".out($data["name"], "json")."</p>";
echo "<p>Age: ".out($data["age"], "json")."</p>";
```

### Example 2: Securing Database Output

```php
echo out($name);
echo out($email);
```

> [!NOTE]
> **Just To Let You Know...**
>
> More details pertaining to the out() function are available from [here](../0130Form_Handling/0600best_practices_for_handling_data.md).


