# Passing Data Into View Files


Passing data into view files in Trongate involves initializing an associative array within a controller and passing it to the view() method. This array contains variables that can be accessed directly within the view for dynamic content rendering.

## Basic Data Passing


The technique for passing data from controller files into view files comprises of the creation of an associative array of key-value pairs. This data array is then passed as the second argument to the view() method:

```php
$data = [
  "first_name" => "John",
  "last_name" => "Smith"
];
$this->view("welcome", $data);
```


This example initializes `$data` with user information and renders the 'welcome' view, where variables like `$first_name` and `$last_name` can be accessed directly.

## Complex Data Types


You can pass various data types such as arrays, objects, and booleans into view files. For instance, consider passing an array of cities and today's date to a view:

```php
function information() {
$cities = ["New York", "London", "Paris"];
$data = [
  "cities" => $cities,
  "today" => "Monday"
];
$this->view("information", $data);
}
```

## Accessing Passed Data


Within view files, accessed data is available as standard variables. For debugging or development purposes, you can use:

```php
var_dump($data);
```


To display structured data in a formatted manner, use Trongate's json() method:

```php
json($data);
```

## Example: Rendering Dynamic Content


Enhance the `greeting()` method to pass a name variable into a view file:

```php
function greeting() {
  $data["name"] = "John";
  $this->view("greeting", $data);
}
```


In the 'greeting.php' view file, you can directly echo the `$name` variable:

```php
<h1>Hello <?= $name ?></h1>
<p>It's nice to see you!</p>
```


Output:

![Screenshot showing greeting message with a name](images/75/hello_john.png)
        
*Screenshot showing greeting message with a name.*
> [!CAUTION]
> **Danger!**
>
> When rendering data from untrusted sources like user inputs, always sanitize outputs to prevent security vulnerabilities. Trongate provides the json() function for safe output encoding, protecting against XSS attacks by properly formatting content for HTML, XML, JSON, JavaScript, and HTML attributes.


