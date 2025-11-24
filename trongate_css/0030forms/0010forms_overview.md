# Forms Overview


Trongate CSS provides elegant, responsive form styling out of the box. Forms are styled automatically without requiring additional classes - just write standard HTML and let Trongate CSS handle the presentation.

## Basic Example


The form below uses **pure HTML** and looks beautiful on both desktop devices and mobile devices.  You may be surprised to discover, there are no classes or special attributes - in the source code - whatsoever.

Name
            

            Email Address
            
            
            Enquiry Type (optional)
            
                Choose an option...
                General Enquiry
                Technical Support
                Billing Question
            
            
            Message
            
            
            Send Message

Here's the source code for the above form:

```html
<form>
    <label>Name</label>
    <input type="text" name="name" placeholder="Your name">

    <label>Email Address</label>
    <input type="email" name="email" placeholder="Your email">
    
    <label>Enquiry Type <span>(optional)</span></label>
    <select name="type">
        <option value="">Choose an option...</option>
        <option value="general">General Enquiry</option>
        <option value="support">Technical Support</option>
        <option value="billing">Billing Question</option>
    </select>
    
    <label>Message</label>
    <textarea name="message" placeholder="Enter your message"></textarea>
    
    <button>Send Message</button>
</form>
```

## Core Features


When you create forms with Trongate CSS, the following styles are automatically applied:


- Forms take up 100% width of their container.
- All form elements receive consistent padding (0.6em) and border-radius (6px).
- Labels are positioned above their form elements with appropriate spacing.
- Focus states are clearly visible using the primary theme color.
- Font sizes and families remain consistent across all elements.
- Forms automatically adapt for mobile devices.

## Form Layout Options


Control form width by wrapping your form in one of Trongate's container classes:

```html
<div class="container-xxs">
    <!-- Perfect for login forms (450px max width) -->
    <form>...</form>
</div>

<div class="container-xs">
    <!-- Good for simple forms (640px max width) -->
    <form>...</form>
</div>

<div class="container-sm">
    <!-- For larger forms (760px max width) -->
    <form>...</form>
</div>
```

> [!NOTE]
> **Just To Let You Know...**
>
> For additional information about containers, see our documentation for [Container Classes](documentation/display/trongate_css/css-fundamentals/container-classes).


## Label Spans


Span elements within labels are automatically styled in green. This is useful for letting users know if a form field is optional.  For example:

Username (optional)
```html
<label>Username <span>(optional)</span></label>
<input type="text">
```

