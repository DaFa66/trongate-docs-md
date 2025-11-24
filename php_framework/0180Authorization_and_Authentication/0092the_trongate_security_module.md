# The Trongate Security Module


The **Trongate Security** module is an essential part of the Trongate framework, included with every installation to help manage authentication, authorization, and other security-related concerns. It provides a centralized hub for handling security tasks, ensuring that only authorized users can access restricted areas and resources within an application. By utilizing the Trongate Security module, developers can implement robust security measures with ease, enhancing overall application security.

## Exploring the Code


The main PHP class for the Trongate Security module is somewhat unusual because it only has one method. Here's the code for the entire `Trongate_security` class (Trongate_security.php):

```php
<?php
class Trongate_security extends Trongate {

  /**
   * Ensures the user is allowed access for the specified scenario.
   *
   * @param string $scenario The scenario for access control. Default is 'admin panel'.
   * @param array $params (Optional) Additional parameters for more granular control.
   * @return string Returns a Trongate token or initializes the 'not allowed' procedure.
   */
  public function _make_sure_allowed(string $scenario = 'admin panel', array $params = []): string {
    // Returns either a Trongate token or initializes the 'not allowed' procedure.

    switch ($scenario) {
      // case 'members area':
      //   $this->module('members');
      //   $token = $this->members->_make_sure_allowed();
      //   break;
      default:
        $this->module('trongate_administrators');
        $token = $this->trongate_administrators->_make_sure_allowed($scenario, $params);
        break;
    }

    return $token;
  }
}
```


The _make_sure_allowed() method accepts two possible arguments:


1. A required `$scenario` (string) argument
2. An optional `$params` (array) argument


The `_make_sure_allowed()` method contains a PHP switch statement. Each item within the switch statement represents a different web application **scenario**, and the class is provided with the expectation that users will add their own scenarios to the switch statement as their application grows.

## Understanding Scenarios


An important concept for those working with the Trongate Security module is **scenarios**.


A **scenario**, in the context of Trongate Security, refers to a general situation or context where usage of the module may be desirable to enforce access control. Scenarios are not tied directly to specific user levels but rather represent broader access contexts that may involve multiple user levels. Below is an assortment of possible scenarios that could be relevant for a web application:


- **Admin Panel:** A restricted area for administrators to manage application settings.
- **Discussion Forum:** A space where users of various levels (e.g., moderators, members, guests) can interact.
- **Private Members Area:** A section of the application accessible only to registered members.
- **Customer Account Page:** A personalized dashboard for customers to view their orders, update their profiles, submit technical support requests, etc.


Scenarios allow developers to define access rules that apply to specific parts of the application, irrespective of the user levels involved. For instance, a discussion forum might be accessible to multiple user levels, such as moderators, members, and even guests, depending on the application's requirements. The scenario itself exists independently of user levels, serving as a general context for access control.


---

## Basic Example: Enforcing Access Control


To enforce access control using the Trongate Security module, you can utilize the _make_sure_allowed() method from any other module. This method ensures that the user has the necessary permissions for a given scenario before proceeding.

### Example: Restricting Access to an Admin Panel


The code below demonstrates how to restrict access to an admin panel by ensuring that only users with an "admin" user level can view it.

```php
<?php
class Admin_panel extends Trongate {

  public function manage(): void {
    // Ensure the user is allowed access to the 'admin panel' scenario.
    $this->module('trongate_security');
    $token = $this->trongate_security->_make_sure_allowed('admin panel');

    // If the user is allowed, load the admin panel view.
    $data['view_module'] = 'admin_panel';
    $data['view_file'] = 'manage';
    $this->load_template($data);
  }
}
```
### Explanation


- **Line 5:** Loads the `trongate_security` module, making its methods available for use.

```php
$this->module('trongate_security');
```

**Line 6:** Invokes the _make_sure_allowed() method with the scenario name `'admin panel'`. This ensures that only users with the appropriate permissions can proceed.```php
$token = $this->trongate_security->_make_sure_allowed('admin panel');
```

**Lines 9-11:** If the user is allowed, the admin panel view is loaded.```php
// If the user is allowed, load the admin panel view.
$data['view_module'] = 'admin_panel';
$data['view_file'] = 'manage'; 
$this->load_template($data);
```

> [!NOTE]
> **Just To Let You Know...**
>
> The scenario of 'admin panel' is the default argument for the _make_sure_allowed() method. This means that the same result could be achieved *without* actively declaring a value of 'admin panel' for the first argument. For example:
> 
> ```php
> $this->module('trongate_security');
> $token = $this->trongate_security->_make_sure_allowed();
> ```


## How the Trongate Administrators Module Interacts with Other Modules


To better understand how the Trongate Security module integrates with other modules, let's delve into the mechanics of the following two lines of code (taken from Trongate_security.php):

```php
$this->module('trongate_administrators');
$token = $this->trongate_administrators->_make_sure_allowed($scenario, $params);
```
### Purpose of These Lines


These two lines of code delegate the mechanics of access control to another module - in this case, the 'Trongate Administrators' module.


Sure enough, within the 'Trongate Administrators' module, there is a method that is *also* named `_make_sure_allowed()`. *That* method makes sure the user is logged in as an administrator by invoking the 'Trongate Tokens' module. If a valid token is found, it is returned. Otherwise, the user is redirected to a login page.


---

## Advanced Example: Granular Access Control in a Discussion Forum


Let's consider a scenario where we have a discussion forum module that allows users to create, edit, and delete comments. However, we want to restrict the editing and deletion of comments to either the user who created the comment or users with administrative privileges.


To achieve this, we can utilize the `$params` argument in the `_make_sure_allowed()` method to pass additional data, such as the `record_id` of the comment being modified and the specific `action` being performed.

### Example: Restricting Comment Editing and Deletion


In this example, we'll assume we have a `Forums` class with a `write_record()` method that handles the updating or deletion of comments.

```php
<?php
class Forums extends Trongate {
  public function write_record($id = null): void {
    // Ensure the user is allowed to edit or delete the comment
    $params = ['record_id' => $id, 'action' => 'write record'];
    $this->module('trongate_security');
    $token = $this->trongate_security->_make_sure_allowed('discussion forum', $params);

    // If the user is allowed, proceed with updating or deleting the comment
    // ...
  }
}
```
### Explanation


- **Line 5:** The `write_record()` method takes an optional `$id` parameter, representing the ID of the comment being edited or deleted.
- **Line 7:** We create a `$params` array containing the `record_id` key-value pair, where the value is the `$id` of the comment, and an `action` key-value pair specifying the action being performed (in this case, 'write record').
- **Line 8:** We load the `trongate_security` module to access its methods.
- **Line 9:** We invoke the `_make_sure_allowed()` method, passing the scenario as `'discussion forum'` and the `$params` array containing the `record_id` and `action`.
- **Lines 11-12:** If the user is allowed to edit or delete the comment based on the scenario, `record_id`, and `action`, the method proceeds with the update or deletion logic.


Implementing a solution like this would require adding an additional **case** to the switch statement within the 'Trongate_security' class.

```php
<?php
class Trongate_security extends Trongate {
  /**
   * Ensures the user is allowed access for the specified scenario.
   *
   * @param string $scenario The scenario for access control. Default is 'admin panel'.
   * @param array $params (Optional) Additional parameters for more granular control.
   * @return string Returns a Trongate token or initializes the 'not allowed' procedure.
   */
  public function _make_sure_allowed(string $scenario = 'admin panel', array $params = []): string {
    // Returns either a Trongate token or initializes the 'not allowed' procedure.
    switch ($scenario) {
      case 'discussion forum':
        $this->module('forum');
        $token = $this->forum->_make_sure_allowed($params);
        break;
      default:
        $this->module('trongate_administrators');
        $token = $this->trongate_administrators->_make_sure_allowed($scenario, $params);
        break;
    }
    return $token;
  }
}
```


By leveraging the `$params` argument and including the `action` property, we can enforce even more granular access control rules within the discussion forum module. This allows us to handle different actions, such as editing or deleting comments, with specific permissions based on the user's role or ownership of the comment.


---

## Addressing Circular Dependency Concerns


At first glance, the pattern employed by the Trongate Security module might raise concerns about circular dependencies. For example, it allows for a scenario where 'Module A' invokes 'Module B', and then 'Module B' invokes a method from within 'Module A'. This circular nature of the code flow could potentially lead to confusion and make the codebase harder to understand.


However, it's important to note that using the Trongate Security module is not a strict requirement. Developers have the option to bypass it altogether, for example, by directly calling the `_make_sure_allowed()` method from the 'Trongate Administrators' module instead.  However, while this approach may seem simpler and more straightforward, it comes with its own set of drawbacks.

### Beware of Spaghetti Code!


Directly calling the `_make_sure_allowed()` method from the 'Trongate Administrators' module would result in a codebase that is more rigid and less adaptable to change. As the application evolves and grows, the rules for managing access to various areas, such as the admin panel, may need to be modified or expanded. Having security-related code scattered throughout different modules - with no common point of entry - can result in a codebase that is challenging to maintain and extremely difficult to upgrade.

### The Benefits Of The Trongate Security Module


By channeling security-related functionality through the Trongate Security module, developers gain a centralized hub for handling all security matters. This centralization promotes code reusability, maintainability, and scalability. It allows for a more flexible and modular approach to managing access control across the entire application.


While the Trongate Security module's approach may introduce some level of indirection and potential for circular dependencies, the benefits it provides in terms of code organization and maintainability outweigh the concerns. By consolidating security-related code into a dedicated module, developers can ensure that access control is handled consistently and can easily adapt to changing requirements.

