# Returning View Output as a Variable


To capture the rendered output of a view file as a string variable in Trongate, developers can utilize the third argument of the view() method. This approach is useful when the output needs to be manipulated or processed further before being sent to the output stream.

## Example Usage


Consider a scenario where you want to capture the HTML output of a 'information.php' view file:

```php
/**
* Retrieve view file output as a string.
*
* @return string The rendered HTML content of the 'information' view file.
*/
private function get_information(): string {
  // Define cities and today's information
  $data['cities'] = ["New York", "London", "Paris"];
  $data['today'] = "Monday";
  // Return the view contents as a string
  $html = $this->view("information", $data, true);
  return $html;
}
```


The code sample above demonstrates capturing the rendered output of a view file and returning the view file output as a PHP variable named, '**$html**'.

## Step-by-Step Guide


1. **Step 1:** Assign the result of the view() method to a variable:
2. **Step 2:** Include the boolean value `true` as the third parameter to return the output as a string:
3. **Step 3:** Complete the method by returning the newly created variable:

> [!TIP]
> **Best Practices**
>
> If no data array is available when calling the view, simply pass an empty array (as a second argument) followed by the boolean, `true`:
> 
> ```php
> $output = $this->view("file", [], true);
> ```
> 
> 
> This technique effectively returns the view content as a string, facilitating flexible handling within the application.


