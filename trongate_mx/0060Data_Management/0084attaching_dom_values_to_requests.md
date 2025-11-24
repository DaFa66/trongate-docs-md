# Attaching DOM Values To Requests


The `mx-dom-vals` attribute in Trongate MX enables you to dynamically attach values from DOM elements to your HTTP requests. This powerful feature allows you to capture and transmit information from specific elements on your page, such as text content or input values.

## Syntax


The `mx-dom-vals` attribute requires a JSON object where each key represents a parameter name and the value is an object containing two properties:


- `selector`: A CSS selector that identifies the target element.
- `property`: The element property to capture (e.g., `innerText`, `value`, `innerHTML`).

## Basic Example


Using Trongate's form helper functions:

```vf
<?php
$btn_attr = [
    'mx-post' => 'api/submit',
    'mx-dom-vals' => '{
        "headline": {
            "selector": "h1",
            "property": "outerHTML"
        }
    }'
];
echo form_button('submit_btn', 'Submit Headline', $btn_attr);
?>
```


Pure HTML equivalent:

```html
<button mx-post="api/submit"
        mx-dom-vals='{
            "headline": {
                "selector": "h1",
                "property": "outerHTML"
            }
        }'>Submit Headline</button>
```


When clicked, this button will:


- Find the first `<h1>` element on the page.
- Capture its outer HTML (including the h1 tags).
- Send this value to the server as a parameter named "headline".

## Real-World Examples

### Example 1: Capturing Paragraph Text


Using Trongate's form helper functions:

```vf
<?php
$btn_attr = [
    'mx-post' => 'api/submit',
    'mx-dom-vals' => '{
        "paragraph_text": {
            "selector": "p.intro",
            "property": "innerText"
        }
    }'
];
echo form_button('submit_btn', 'Submit Text', $btn_attr);
?>
```


Pure HTML equivalent:

```html
<button mx-post="api/submit"
        mx-dom-vals='{
            "paragraph_text": {
                "selector": "p.intro",
                "property": "innerText"
            }
        }'>Submit Text</button>
```

### Example 2: Using json_encode with PHP Arrays


Using Trongate's form helper functions:

```vf
<?php
$dom_vals = [
    'user_input' => [
        'selector' => 'input[name="username"]',
        'property' => 'value'
    ]
];

$btn_attr = [
    'mx-post' => 'api/submit',
    'mx-dom-vals' => json_encode($dom_vals)
];
echo form_button('submit_btn', 'Submit Input', $btn_attr);
?>
```


Pure HTML equivalent:

```html
<button mx-post="api/submit"
        mx-dom-vals='{
            "user_input": {
                "selector": "input[name=\"username\"]",
                "property": "value"
            }
        }'>Submit Input</button>
```

### Example 3: Capturing Multiple Elements


Using Trongate's form helper functions:

```vf
<?php
$dom_vals = [
    'headline' => [
        'selector' => 'h1',
        'property' => 'innerText'
    ],
    'summary' => [
        'selector' => 'p.intro',
        'property' => 'innerText'
    ],
    'selected_value' => [
        'selector' => '#options',
        'property' => 'value'
    ]
];

$form_attr = [
    'mx-post' => 'articles/submit',
    'mx-dom-vals' => json_encode($dom_vals)
];
echo form_open('#', $form_attr);
echo form_submit('submit_btn', 'Submit Article');
echo form_close();
?>
```


Pure HTML equivalent:

```html
<form mx-post="articles/submit"
      mx-dom-vals='{
          "headline": {
              "selector": "h1",
              "property": "innerText"
          },
          "summary": {
              "selector": "p.intro",
              "property": "innerText"
          },
          "selected_value": {
              "selector": "#options",
              "property": "value"
          }
      }'>
    <button type="submit">Submit Article</button>
</form>
```

## Available Properties


You can use any of these properties in your mx-dom-vals:


- `value`: Gets the current value (best for form inputs).
- `innerText`: Gets the text content only.
- `innerHTML`: Gets the HTML content inside the element.
- `outerHTML`: Gets the entire element including its HTML tags.

## Server-Side Handling


The captured values are accessible in your controller using the post() function:

```vf
<?php
public function submit() {
    $headline = post('headline');         // From mx-dom-vals
    $paragraph_text = post('paragraph_text');   // From mx-dom-vals
    $selected_value = post('selected_value');   // From mx-dom-vals
    
    // Process the values...
}
?>
```

> [!TIP]
> **Best Practices**
>
> 1. **Use Specific Selectors**
>         
> - Prefer IDs and unique class names.
> - Avoid relying on element position or order.
> 
> 
>     
> 2. **Choose Appropriate Properties**
>         
> - Use `value` for form inputs.
> - Use `innerText` for capturing text content.
> - Use `innerHTML` when HTML markup is needed.
> 
> 
>     
> 3. **Validation**
>         
> - Always validate captured values server-side.
> - Don't trust DOM values for critical operations.
> - Apply appropriate sanitization for HTML content.


## Common Pitfalls


- Invalid selectors will cause the value to be omitted.
- Missing elements will be silently ignored.
- Malformed JSON will prevent all values from being captured.
- GET requests do not support mx-dom-vals.

## Summary


The `mx-dom-vals` attribute provides a powerful way to capture and transmit DOM values with your HTTP requests. By using specific selectors and appropriate properties, you can easily include dynamic page content in your form submissions. Remember to use `json_encode()` when working with complex values and always validate the captured data server-side.

