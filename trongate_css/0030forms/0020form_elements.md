# Form Elements


This guide explores the various form elements available in Trongate CSS and demonstrates their behaviors, states, and common usage patterns.

## Input Field States


Every form input has multiple visual states to provide clear user feedback:


```html
<!-- Default state -->
<input type="text" placeholder="Default state">

<!-- Focused state (click to see) -->
<input type="text" placeholder="Click here to see focus state">

<!-- Disabled state -->
<input type="text" placeholder="This input is disabled" disabled>
```

## Input Type Variations


Different input types provide specialized functionality while maintaining consistent styling:

Search with ValidationNumbers with Controls
```html
<label>Search with Validation</label>
<input type="search" required placeholder="Enter search term...">

<label>Numbers with Controls</label>
<input type="number" min="0" max="100" value="50">
```

## Select Elements


Select dropdowns support option grouping for better organization:

Select with Option Groups
            Choose an option...
            
                Apple
                Orange
                Banana
            
            
                Carrot
                Broccoli
                Spinach
```html
<label>Select with Option Groups</label>
<select>
    <option value="">Choose an option...</option>
    <optgroup label="Fruits">
        <option>Apple</option>
        <option>Orange</option>
        <option>Banana</option>
    </optgroup>
    <optgroup label="Vegetables">
        <option>Carrot</option>
        <option>Broccoli</option>
        <option>Spinach</option>
    </optgroup>
</select>
```

## Textarea Variations


Textareas can be configured for different use cases:

Quick NotesDetailed Description
```html
<label>Quick Notes</label>
<textarea rows="2" placeholder="Short message..."></textarea>

<label>Detailed Description</label>
<textarea rows="5" placeholder="Enter a longer description..."></textarea>
```

## Input Groups


In the example below, two buttons are positioned side-by-side by adding the `.flex-row` class to a containing element.



Below is the source code for the example shown above.  Notice how the second form field contains a class of `.ml-1`.  The purpose of this additional class is to add a left margin (with a value of '1em') onto the second form field element, thereby creating a small gap between the two form fields.

```html
<div class="flex-row">
    <input type="text" name="first_name" placeholder="First Name...">
    <input type="text" class="ml-1" name="last_name" placeholder="Last Name...">
</div>
```

### Horizontal Search Bar


The example below uses `.flex-row`, a little custom CSS to produce an attractive horizontal search bar.  The search button contains a [Font Awesome](https://fontawesome.com/) icon.   The icon depicts a small magnifying glass (a commonly used icon for submit buttons that appear on search forms).

**
```html
<div class="flex-row">
    <input type="search" id="search-input" placeholder="Search..." class="mb-0"> 
    <button class="mt-0" id="search-btn"><i class="fa fa-search"></i></button>
</div>
<style>
#search-input {
    border-top-right-radius: 0;
    border-bottom-right-radius: 0;
}

#search-btn {
    border-top-left-radius: 0;
    border-bottom-left-radius: 0;
    max-width: min-content;
}
</style>
```

> [!NOTE]
> **Just To Let You Know...**
>
> To get the magnifying glass icon appearing, you'll have to load Font Awesome into your webpage.   This can be achieved by adding the following line of code onto the `<head>` section of your webpage:
> 
> ```html
> <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
> ```


## Checkbox and Radio Groups


Checkboxes and radio buttons can be organized into intuitive groups:

Choose Your Interests
Technology Sports Travel

        
            Select Your Role
Developer Designer Manager
```html
<fieldset>
    <label>Choose Your Interests</label>
    <div>
        <label><input type="checkbox"> Technology</label>
        <label><input type="checkbox"> Sports</label>
        <label><input type="checkbox"> Travel</label>
    </div>
</fieldset>

<fieldset>
    <label>Select Your Role</label>
    <div>
        <label><input type="radio" name="role"> Developer</label>
        <label><input type="radio" name="role"> Designer</label>
        <label><input type="radio" name="role"> Manager</label>
    </div>
</fieldset>
```

### Alternative Example


The example below uses classes of `.mb-0` and `.mt-0` to adjust top and bottom margins.  The result is a more compact assortment of form elements.

Subscribe to newsletter 
---

One 
      Two 
      Three 
      Four
```html
<div>
  <label>
    <input type="checkbox" id="newsletter">Subscribe to newsletter</label>
  <hr>
  <div>
    <label>One <input type="radio" checked="checked" name="radio" class="mt-0 mb-0">
    </label>
    <label>Two <input type="radio" name="radio" class="mt-0 mb-0">
    </label>
    <label>Three <input type="radio" name="radio" class="mt-0 mb-0">
    </label>
    <label>Four <input type="radio" name="radio" class="mt-0 mb-0">
    </label>
  </div>
</div>
```

