# Regarding Coding Style


The Trongate framework minimizes overheads to achieve best-in-class performance. This philosophy extends to its coding style, focusing on three primary goals:


- **Maximize Developer Productivity:** Achieve more with fewer lines of code.
- **Embrace Pure PHP Syntax:** Mirror the familiarity of native PHP conventions.
- **Minimize Ambiguity:** Use clear naming conventions to reduce errors.

## Modern PHP for Enhanced Web Development


The Trongate framework's core resides in the 'engine' directory. All functions and methods within this directory include doc blocks, access modifiers (public/private/protected), type hinting, and return types, ensuring well-documented, modern PHP syntax.


Despite this, Trongate introduces unique syntax nuances that distinguish it from other frameworks.

## Aligning PHP with C Roots


Trongate aims to provide a coding experience akin to pure PHP. Code examples in this documentation follow the K&R (Kernighan and Ritchie) coding style.


K&R is a compact, unambiguous style commonly used in C programming. It is named after Brian Kernighan and Dennis Ritchie, authors of "The C Programming Language."

> [!NOTE]
> **Just To Let You Know...**
>
> **Note:** PHP's origins in C influence its syntax, including the prevalence of snake_case function names—a convention Trongate adopts.


### Key Characteristics of K&R Style


- Indentation uses two spaces, not tabs, for consistency.
- Opening curly braces '{' appear on the same line as the function or control statement.
- Closing curly braces '}' align with the start of the controlling statement.

### Example

```php
function hello_world() {
  echo "hello world";
}
```

## Additional Coding Conventions


Trongate promotes the following practices:


- Use snake_case for function, file, and directory names.
- Prefer plural names for collections or groups.
- Adopt two-space indentation for clarity.

> [!NOTE]
> **Just To Let You Know...**
>
> Trongate's syntax mirrors PHP's core conventions, such as snake_case, ensuring familiarity and consistency for developers.


## Snake Case for Clarity


Trongate's use of snake_case reduces ambiguity, unlike camelCase conventions in languages like JavaScript. For example, `getElementById()` versus `getElementByID()` can confuse developers. Snake_case eliminates such issues by using lowercase letters and underscores, e.g., `get_element_by_id`.


This approach simplifies development, reduces cognitive load, and prevents common errors.

## Minimal Use of Namespaces and Access Modifiers


Trongate streamlines development by minimizing namespaces and access modifiers. This contrasts with traditional PHP frameworks but accelerates development processes.


While optional, many developers find this approach enhances efficiency once adopted.

## Modern PHP Features


PHP 8 introduces features like type hinting, doc-blocks, return types, and constructor property promotion. These enhance code clarity and robustness but remain optional.


Trongate supports these features but generally avoids them in documentation to maintain simplicity and accessibility for new developers.

> [!TIP]
> **Best Practices**
>
> Developers familiar with modern PHP features are encouraged to use them to improve code quality and maintainability.
> 
> 
> For example, consider the following PHP method:
> 
> ```php
> function greeting($name, $age) {
>   if ($age < 18) {
>     return 'Hi, '.$name.'! You are young and full of potential.';
>   } elseif ($age >= 18 && $age < 65) {
>     return 'Hi, '.$name.'! You are in your prime years.';
>   } else {
>     return 'Hi, '.$name.'! You have gained wisdom with age. Respect!';
>   }
> }
> ```
> 
> 
> The above syntax works without any issues. However, with modern PHP, it is possible to enhance the method by adding access modifiers, doc blocks, type hinting, and return types. For example:
> 
> ```php
> /**
>  * Generates a personalized greeting message based on the user's name and age.
>  *
>  * @param string $name The name of the person being greeted.
>  * @param int $age The age of the person.
>  * 
>  * @return string A personalized greeting message.
>  */
> public function greeting(string $name, int $age): string {
>   if ($age < 18) {
>     return 'Hi, '.$name.'! You are young and full of potential.';
>   } elseif ($age >= 18 && $age < 65) {
>     return 'Hi, '.$name.'! You are in your prime years.';
>   } else {
>     return 'Hi, '.$name.'! You have gained wisdom with age. Respect!';
>   }
> }
> ```
> 
> 
> To be clear, readers are encouraged to use modern PHP syntax where possible. However, for the purposes of brevity and clarity, code samples will be kept as simple as possible throughout this documentation.


## Conclusion


Trongate's syntax differs significantly from other PHP frameworks through streamlined practices, unique naming conventions, and concise coding. These deliberate choices prioritize efficiency and error reduction.


By refining coding practices, Trongate enhances developer productivity and advances PHP development through thoughtful innovation.

