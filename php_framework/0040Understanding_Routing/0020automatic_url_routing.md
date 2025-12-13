# Automatic URL Routing


Trongate's automatic routing system follows a simple, predictable pattern to map URLs to your code. When Trongate receives a URL request, it breaks the URL into segments and uses these segments to determine which code to run.

## How URL Segments Work


Consider this example URL:

```
https://example.com/members/profile/88
```


Trongate splits this URL into three segments and uses them in a specific way:


| Segment | Example | Purpose |
| ---|---|---|
| First Segment | `members` | Names both the module folder and the controller to use |
| Second Segment | `profile` | Names the method to run |
| Third Segment | `88` | Passed as a parameter to the method (optional) |


Given the URL above, Trongate will:


1. Look for a 'members' module folder
2. Find the 'Members' controller inside that folder
3. Run the 'profile' method
4. Pass '88' as a parameter to that method

### Mapping URLs to Code


Here's what the corresponding code, based on our example, could look like:

```php
<?php
class Members extends Trongate {

    public function profile($user_id) {
        // $user_id will be 88
        // Your code here...
    }

}
```

## Important Rules


- Module folders should be lowercase (e.g., 'members')
- Controller class names should have an uppercase first character (e.g., 'Members')
- Method names should be lowercase (e.g., 'profile')
- If no second segment exists, Trongate will look for an 'index' method

> [!NOTE]
> **Just To Let You Know...**
>
> [Custom URL routing](0026introducing_custom_url_routing.md) will override automatic routing. If you have defined a custom route for a URL, *that* will take precedence over the automatic routing rules described here.


## In Summary


Automatic routing makes it easy to add new functionality to your application - just create the appropriate module, controller, and methods, and Trongate will automatically make them accessible via URLs that follow this pattern.

