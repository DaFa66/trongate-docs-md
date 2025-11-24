# Targeting Elements


The `mx-target` attribute in Trongate MX is a powerful feature that allows you to specify which element in the DOM should be updated with the server response. This enables fine-grained control over where and how content is dynamically inserted or replaced, enhancing the interactivity and responsiveness of your web application without writing JavaScript.


If no `mx-target` attribute is specified, Trongate MX will automatically update the triggering element itself with the server response.

## Basic Element Targeting:


With the code below, the response from the server will be inserted into the `<div>` element with the id "result". You can use any valid CSS selector to target elements.


Here's how to achieve this using Trongate's form_button() form helper:

```vf
<?php
$btn_attr = [
  'mx-get' => 'api/data',
  'mx-target' => '#result'
];
echo form_button('get_data_btn', 'Get Data', $btn_attr);
?>

<div id="result"></div>
```


Alternatively, the same functionality can be built with pure HTML as shown below.

```html
<button mx-get="api/data" 
        mx-target="#result">Get Data</button>

<div id="result"></div>
```

## Advanced Element Targeting


The `mx-target` attribute supports several advanced targeting options to provide more flexibility:


| Option | Description | Example Syntax |
| ---|---|---|
| CSS Selector | Any valid CSS selector that targets a specific element. | `mx-target="#myDiv"` |
| closest <selector> | Finds the closest ancestor matching the selector. | `mx-target="closest li"` |
| find <selector> | Finds the first descendant matching the selector. | `mx-target="find .target"` |
| none | Makes the request without updating any content. | `mx-target="none"` |

## More Examples:

### Finding the First Descendant (find <selector>):


In this example, when the form is submitted, the server response will be inserted into the `.status-message` div that exists within the form. The `find` selector locates the **first descendant element** matching the given selector, making it perfect for updating specific parts within a larger component.


Using Trongate's form helper functions:

```vf
<?php
$form_attr = [
    'mx-post' => 'api/submit-data',
    'mx-target' => 'find .status-message'
];
echo form_open('#', $form_attr);
echo form_label('Title');
echo form_input('title', '');
echo form_submit('submit', 'Save');
?>
<div class="status-message">
    Ready to submit...
</div>
<?= form_close() ?>
```


Here's an alternative syntax, written in pure HTML:

```html
<form mx-post="api/submit-data" 
      mx-target="find .status-message">
    <label>Title</label>
    <input type="text" name="title">
    <button type="submit">Save</button>
    <div class="status-message">
        Ready to submit...
    </div>
</form>
```

### Finding the Closest Ancestor (closest <selector>):


The `closest` selector finds and updates the **nearest parent element** that matches the given selector. This is particularly useful when you need to update a containing element from a control that's nested within it.


Here's an example that uses Trongate's form_button() form helper:

```vf
<?php
$btn_attr = [
  'mx-get' => 'api/data',
  'mx-target' => 'closest div'
];
echo form_button('load_btn', 'Load Content', $btn_attr);
?>
```


And here's how the same result can be achieved with pure HTML:

```html
<button mx-get="api/data" 
        mx-target="closest div">Load Content</button>
```

### Using Tag Selectors:


You can target any HTML element using its tag name as a selector (e.g., 'body', 'main', 'footer'). The server response will replace the entire contents of the **first matching element** on the page.


Using Trongate's form_button() form helper:

```vf
<?php
$btn_attr = [
  'mx-get' => 'api/data',
  'mx-target' => 'body'
];
echo form_button('load_btn', 'Load Content', $btn_attr);
?>
```


If you'd rather work directly with HTML, here's the code:

```html
<button mx-get="api/data" 
        mx-target="body">Load Content</button>
```

### No Content Replacement (none):


When `mx-target="none"` is specified, the server request will be made but no content will be updated on the page. This is useful when you need to trigger a server action without needing to update the UI, such as logging events or performing background tasks.


Here's an example, using Trongate's form_button() form helper:

```vf
<?php
$btn_attr = [
  'mx-get' => 'api/data',
  'mx-target' => 'none'
];
echo form_button('no_replacement_btn', 'No Replacement', $btn_attr);
?>
```


Here's how the same result can be achieved with pure HTML:

```html
<button mx-get="api/data" 
        mx-target="none">No Replacement</button>
```

