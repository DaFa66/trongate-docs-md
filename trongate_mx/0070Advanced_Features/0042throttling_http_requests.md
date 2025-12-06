# Throttling HTTP Requests


The `mx-throttle` attribute in Trongate MX allows you to limit the frequency of HTTP requests triggered by user interactions. This feature helps optimize performance and reduce server load by preventing rapid successive requests.

## Usage


Set the `mx-throttle` attribute on an element to specify the minimum time (in milliseconds) that must pass between successive requests.

### Basic Example:

```vf
<?php 
$attr = [
  'mx-get' => 'api/search',
  'mx-trigger' => 'input',
  'mx-throttle' => '300',
  'mx-target' => '#results'
];

form_input('search', '', $attr);
?>
```


Here's the same solution, written in pure HTML:

```html
<input type="text" name="search" 
       mx-get="api/search" 
       mx-trigger="input" 
       mx-throttle="300" 
       mx-target="#results">
```


In this example, search requests are throttled to a maximum of one request every 300 milliseconds, even if the user types faster.

> [!NOTE]
> **Just To Let You Know...**
>
> The 'input' event is a standard DOM event that fires when the value of an `<input>`, `<select>`, or `<textarea>` element has been changed. It's particularly useful for tracking changes to form fields in real-time. Here are some key points about the 'input' event:
> 
> 
> 1. **Real-time tracking:** Unlike the 'change' event, which typically fires when the element loses focus, the 'input' event fires immediately whenever the value changes.
> 2. **Covers multiple input methods:** It triggers for various types of input, including:
> 
> - Typing on a keyboard
> - Pasting text (via mouse or keyboard)
> - Drag-and-drop actions
> - Speech input
> - Autocomplete suggestions
> 
> 
> 3. **Works with different input types:** It's not just for text inputs. It works with other input types like number, range, color, etc.
> 4. **Doesn't fire for all changes:** The 'input' event doesn't fire for changes that don't alter the element's value, like hitting the shift or ctrl keys.
> 5. **Can't be canceled:** Unlike some other events, the 'input' event can't be canceled. It's purely informative.
> 
> 
> Here's a simple example of how it might be used in vanilla JavaScript:
> 
> ```javascript
> const inputElement = document.querySelector('#myInput');
> 
> inputElement.addEventListener('input', function(e) {
>   console.log('Input value changed to: ' + this.value);
> });
> ```
> 
> 
> In the context of an autocomplete feature, using the 'input' event allows Trongate MX to react immediately to any changes in the input field, making it ideal for triggering suggestion requests as the user types.
> 
> 
> The 'input' event is widely supported across modern browsers and provides a more responsive user experience compared to events like 'keyup' or 'change' for this kind of functionality.


## How It Works


When an event that would normally trigger a request occurs:


1. Trongate MX checks if the time since the last request is greater than or equal to the throttle time.
2. If sufficient time has passed, the request is made and the timestamp is updated.
3. If not enough time has passed, the request is skipped.

## Use Cases


- **Search-as-you-type**: Limit API calls while still providing responsive suggestions.
- **Form validation**: Prevent excessive server-side validation requests during rapid user input.
- **Auto-saving**: Implement efficient auto-save functionality without overwhelming the server.
- **Infinite scrolling**: Control the rate of content loading requests as the user scrolls.

## Considerations

> [!TIP]
> **Best Practices**
>
> - **Choose appropriate throttle times**: Balance between responsiveness and server load. Typical values range from 200ms to 1000ms.
> - **Combine with debouncing**: For some use cases, client-side debouncing in addition to throttling can provide better user experience.
> - **Feedback to users**: Consider providing visual feedback when requests are throttled to maintain a responsive feel.
> - **Server-side considerations**: Implement server-side rate limiting as well for comprehensive protection against excessive requests.


### Advanced Example: Throttled Country Search Input


The code below demonstrates a throttled text input that updates country suggestions as the user types, with a minimum interval of 300ms between POST requests. In this example, the typed phrase is sent as 'country' in the request body.

```vf
<?php
echo form_open('countries/submit_country');

$input_attr = [
    'list' => 'countries',
    'mx-post' => 'countries/submit_country',
    'mx-throttle' => '300',
    'mx-trigger' => 'input',
    'mx-target' => '#countries'
];

echo form_input('country', '', $input_attr);
echo '<datalist id="countries"></datalist&gt';
echo form_close();
?>
```


Prefer HTML over helper functions? Here's the equivalent solution:

```html
<form action="countries/submit_country" method="post">
    <input type="text" 
           name="country"
           list="countries"
           mx-post="countries/submit_country"
           mx-throttle="300"
           mx-trigger="input"
           mx-target="#countries">
    <datalist id="countries"></datalist>
</form>
```

> [!TIP]
> **Best Practices**
>
> If you intend to use Trongate's  to perform server-side form validation tests then usage of the  method is essential since it generates a hidden CSRF token input field as well as a closing form tag.


### Explanation of Key Attributes:


- `mx-post="countries/submit_country"`: Specifies that a POST request should be made to the 'submit_country' method of the 'countries' controller.
- `mx-throttle="300"`: Limits the frequency of requests to one every 300 milliseconds.
- `mx-trigger="input"`: Triggers the request on every input event (i.e., when the user types or modifies the input).
- `mx-target="#countries"`: Specifies that the response should update the element with the id "countries" (the datalist in this case).


This example uses HTML5's `datalist` element, which provides a built-in autocomplete feature. As the user types, the datalist is populated with matching country suggestions.

### How It Works:


1. As the user types in the form field, it triggers the 'input' event.
2. Trongate MX checks if 300ms have passed since the last request. If not, it skips the request.
3. If 300ms have passed, a POST request is sent to the 'submit_country' method of the 'countries' controller.
4. The server processes the request and returns a list of matching countries.
5. The response updates the `datalist` element, providing autocomplete suggestions to the user.

> [!NOTE]
> **Just To Let You Know...**
>
> In instances where an element invokes a form submission (for example, by usage of `mx-post`) and the element is within a form, Trongate MX will automatically fetch all of the values within the form and send those to the endpoint as posted values. This mimics standard form submission behavior. As a result, there is no requirement to use the `mx-vals` attribute in this instance, as all form data is automatically included in the HTTP request.


### Server-Side Implementation:


Here's an example of how the controller method might be implemented in Trongate:

```php
public function submit_country() {
  // Retrieve the posted country from the POST request.
  $country = post('country', true);

  if ($country === '') {
    http_response_code(200);
    die(); // If empty field was posted, suggestions element will be emptied.
  }

  // Append the wildcard '%' for the LIKE query and prepare the parameter array for the query.
  $params['country'] = $country.'%';

  // Define the SQL query with a named parameter for the LIKE clause.
  $sql = "SELECT * FROM country WHERE country LIKE :country";

  // Execute the query using query_bind and fetch the results as objects.
  $data['rows'] = $this->model->query_bind($sql, $params, 'object');

  // Load the view with the query results.
  $this->view('autocomplete_suggestions', $data);
}
```


This method performs the following steps:


1. Retrieves the posted 'country' value using Trongate's post() helper function.
2. If the posted value is empty, it returns a 200 status code with an empty response body, which will clear the suggestions.
3. Constructs an SQL query to find countries that start with the posted 'country' value.
4. Executes the query using Trongate's Model class query_bind() method, which handles parameter binding for security.
5. Loads a view file ('autocomplete_suggestions.php') to display the results as datalist options.

### View File (autocomplete_suggestions.php):


The view file, containing the list of potential matches, is rendered by invoking the view() method.

```php
$this->view('autocomplete_suggestions', $data);
```


Inside the view file, a simple FOR loop is used to display the results, from our database query, as `option` elements for the datalist:

```vf
<?php
foreach($rows as $row) {
  echo '<option value="'.$row->entity_title.'">'.PHP_EOL;
}
?>
```


This generates a list of `option` elements, one for each matching country, which will be used as autocomplete suggestions in the datalist.

> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** This approach uses HTML5's `datalist` element, which provides built-in autocomplete functionality. It's particularly efficient for smaller datasets (typically less than 1000 items) and offers a native user experience across modern browsers. For more information, visit [W3Schools - datalist](https://www.w3schools.com/tags/tag_datalist.asp).


## Additional Notes


- The `mx-throttle` attribute is processed client-side and does not require server-side configuration.
- Throttling is applied globally across all elements using the same throttle time.
- If no `mx-throttle` attribute is specified, requests are not throttled and will be sent for every triggering event.
- Throttling works in conjunction with other Trongate MX attributes like `mx-trigger`, `mx-get`, and `mx-target`.

## Summary


By using the `mx-throttle` attribute, you can create more efficient and performant web applications with Trongate MX, ensuring smooth user experiences while managing server load effectively.

