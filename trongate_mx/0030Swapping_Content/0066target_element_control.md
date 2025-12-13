# Target Element Control


The `mx-target-loading` attribute lets you control how [target elements](../0020Core_HTTP_Operations/0040targeting_elements.md) behave during HTTP requests. You can either temporarily hide elements or swap their content with loading messages while waiting for the server to respond.

## Usage


Here's a simple example showing how to use the `mx-target-loading` attribute:

```vf
&lt;?php
$attributes = [
   'mx-get' => 'api/data',
   'mx-target' => '#result',
   'mx-target-loading' => 'cloak'
];

echo form_button('fetch_btn', 'Fetch Data', $attributes);
?&gt;

&lt;div id="result"&gt;This content will be hidden during the request&lt;/div&gt;
```


In this example, when the button is clicked the content inside the result div will temporarily disappear while new data is being fetched. Once the request completes, the new content will appear.


You can achieve the same result, using pure HTML, with the following code:

```html
<button mx-get="api/data"
        mx-target="#result"
        mx-target-loading="cloak">Fetch Data</button>

&lt;div id="result"&gt;This content will be hidden during the request&lt;/div&gt;
```


Use the style of syntax that you like best!

## Two Ways to Handle Loading States

### 1. Hiding Content (Cloaking)

```vf
&lt;?php
$attributes = [
   'mx-get' => 'api/users',
   'mx-target' => '#user-list',
   'mx-target-loading' => 'cloak'
];

echo form_button('users_btn', 'Load Users', $attributes);
?&gt;

<div id="user-list">User list will disappear during loading</div>
```


Here's how the same result can be achieved using pure HTML:

```html
<button mx-get="api/data"
        mx-target="#user-list"
        mx-target-loading="cloak">Fetch Data</button>

<div id="result">User list will disappear during loading</div>
```


Using `cloak` temporarily hides the target element while the request is in progress. This is perfect for hiding forms when an HTTP request has been invoked.

### 2. Showing a Loading Message

```vf
&lt;!-- Hidden placeholder --&gt;
&lt;div id="loading-message" style="display: none;"&gt;
   &lt;div class="blink"&gt;Loading your data...&lt;/div&gt;
&lt;/div&gt;

&lt;?php
$attributes = [
   'mx-get' => 'api/data',
   'mx-target' => '#content',
   'mx-target-loading' => '#loading-message'
];

echo form_button('load_btn', 'Load Content', $attributes);
?&gt;

<div id="content">Original content here</div>
```


This approach replaces the target's content with a loading message during the request. Once the request completes, the new content replaces the loading message.


Here's a pure HTML example that accomplishes the same goal:

```html
<!-- Hidden placeholder -->
<div id="loading-message" style="display: none;">
   <div class="blink">Loading your data...</div>
</div>

<button mx-get="api/data"
        mx-target="#content"
        mx-target-loading="#loading-message">Load Content</button>

<div id="content">Original content here</div>
```

> [!TIP]
> **Best Practices**
>
> PHP is extremely fast!  When testing this kind of functionality, it's advisable to use PHP's in-built `sleep()` function - on your API endpoints.   Doing so, provides an opportunity to clearly see if your application is behaving as expected during HTTP requests.
> 
> 
> Here's an example of how you could use PHP's `sleep()` function to force an API endpoint to wait two seconds before responding to a request:
> 
> ```php
> function test() {
>    sleep(2); // wait for two seconds!
>    echo 'Hello!';
> }
> ```


## Important Implementation Notes

### 1. Hiding Placeholders


Always hide placeholder elements using `style="display: none"`:


** Correct:

```html
&lt;div id="loading" style="display: none;"&gt;Loading...&lt;/div&gt;
```


** Incorrect:

```html
&lt;div id="loading"&gt;Loading...&lt;/div&gt;
```

### 2. Placeholder Content Structure


When using placeholders, remember that only the inner HTML is transferred:


** Correct:

```html
&lt;div id="loading" style="display: none"&gt;
   &lt;div class="blink"&gt;*** PLEASE WAIT ***&lt;/div&gt;
&lt;/div&gt;
```


** Incorrect:

```html
&lt;div id="loading" class="blink" style="display: none"&gt;
   *** PLEASE WAIT ***
&lt;/div&gt;
```

> [!NOTE]
> **Just To Let You Know...**
>
> When using Trongate CSS, any content that is contained within an element with a class of 'blink' will alternately fade in and out with a smooth easing effect, creating a blinking animation that repeats infinitely.  Here's an example of a paragraph that has a class of 'blink' applied:
> 
> 
> I'm having a blinking good time!
> 
> 
> **Understanding The CSS**
> 
> 
> The above is achieved with the following code:
> 
> ```html
> <p class="text-center blink">I'm having a blinking good time!</p>
> ```
> 
> 
> The CSS class of 'text-center' aligns the text to the center of the containing element.   The CSS class of 'blink' makes the text fade in and out infinitely.
> 
> 
> **IMPORTANT NOTE: **In HTML, it's perfectly acceptable to stack multiplate CSS class names on *one* element like so;
> 
> ```html
> <p class="class1 class2 class3">Ahoy!</p>
> ```


## Using Target Control with Out-of-Band Swaps


When you combine `mx-target-loading` with `mx-select-oob` and `mx-target="none"`, you can create sophisticated loading patterns that update multiple elements while providing visual feedback.

```html
<div id="dashboard-container" 
     mx-get="api/dashboard_data" 
     mx-target="none" 
     mx-select-oob='[
         {"select": ".visitors-data", "target": "#visitors-panel"},
         {"select": ".revenue-data", "target": "#revenue-panel"}
     ]'>
    
    <div id="visitors-panel">
        <div class="spinner"></div>
    </div>
    
    <div id="revenue-panel">
        <div class="spinner"></div>
    </div>
</div>

<button onclick="window.TrongateMX.startPolling(document.querySelector('#dashboard-container'), '10s')">
    Start Auto-Refresh
</button>
```


In this example, the container element uses `mx-target="none"` to indicate that it shouldn't be updated directly. Instead, the OOB swaps update the individual panels while each panel displays a spinner until its content loads.


This pattern is particularly useful for dashboards, real-time updates, and polling scenarios where you need to update multiple elements independently while maintaining a clean user experience.

## Conclusion


The `mx-target-loading` attribute in Trongate MX provides a means of controlling the target element *during* an HTTP request.  During an HTTP request, the `mx-target-loading` attribute can:


1. **Swap** in the inner contents of the target element.
2. **Hide** the target element entirely.


Since the attribute has a *swapping* capability, it has been added onto this chapter which has the title, '**Swapping Content**'.  However, it's worth noting that Trongate MX has a variety of other attributes that can be used to control application appearance *during* HTTP requests.  More details regarding those *other* attributes can be found in  [this chapter](../0040Events_and_Responses) and also in the [Trongate MX Attribute Reference](../0080Reference/2000trongate_mx_attributes.md).

