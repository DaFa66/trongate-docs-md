# The Underscore Naming Convention


Trongate employs the underscore naming convention as a mechanism to control method accessibility. This convention involves prefixing method names with an underscore character to prevent them from being accessed directly via a URL.  For example:

```php
public function _calculate_tax($price) {
    $tax = $price * $this->tax_rate;
    return $tax;
}
```


Methods prefixed with an underscore are effectively restricted from public URL invocation, while still remaining accessible within the framework's modular architecture.

## How It Works


In Trongate, modules are designed to be independent yet interoperable. Developers can easily load one module from another, as demonstrated in the example below:

```php
// Load module_b
$this->module('module_b');

// Invoke greeting() method (which resides in module_b)
$this->module_b->greeting();
```

> [!NOTE]
> **Just To Let You Know...**
>
> Information regarding how modules can load and use *other* modules is provided within the, [Modules Calling Modules](../0080Modules_Calling_Modules) chapter of this documentation.



While methods prefixed with an underscore cannot be accessed via a URL, they remain fully accessible within the framework. This ensures that developers can invoke methods across modules without exposing sensitive functionality to external requests.

## Addressing Common Misconceptions


A common misconception is that the underscore naming convention renders methods "private" or "protected." However, this is not the case. In object-oriented programming:


- **Private methods** can only be invoked within their containing class.
- **Protected methods** can be accessed by their containing class and any classes that extend it.


Since modules in Trongate are entirely independent, invoking a method from one module in another would be impossible unless the method is explicitly declared as `public`. The underscore naming convention does not alter a method's visibility within the codebase; rather, it restricts direct URL access to ensure security and maintainability.


Some developers mistakenly associate the underscore naming convention with outdated practices, particularly because earlier PHP frameworks (e.g., Zend Framework 1, early versions of CodeIgniter, and Yii1) used similar approaches but later replaced them with full access modifiers. However, this assumption is incorrect and reflects a misunderstanding of Trongate's unique architecture. **The underscore naming convention is a deliberate and integral part of the framework's design, not a relic of outdated practices.**


Without this convention, developers would need to rely on additional configuration mechanisms, such as YAML files, to explicitly specify which methods can or cannot be accessed via URLs. The underscore naming convention simplifies this process, providing a clean and efficient way to secure methods from direct URL access.

> [!NOTE]
> **Just To Let You Know...**
>
> More information pertaining to this topic is offered [here](../0040Understanding_Routing/0050securing_methods_from_url_access.md).


