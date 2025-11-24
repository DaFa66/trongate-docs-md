# Introduction to Templates


Trongate uses pure PHP for rendering web pages, providing a straightforward and flexible approach to templating. This section explains the role of templates, how they differ from views, and how they operate within the Trongate framework.

## What Are Templates?


In Trongate, a template is a PHP file that defines the complete structure of an HTML web page. Templates ensure consistency across an application by incorporating common elements—such as headers, footers, and navigation menus—into every page.

## Templates vs. Views


It is essential to understand the distinction between templates and views:


- **Templates:** Define the full structure of a web page, including the `<!DOCTYPE>`, `<html>`, `<head>`, and `<body>` tags. They often include reusable components like headers, footers, and sidebars.
- **Views:** Contain partial content that is injected into a template. A view typically represents a specific section of a page rather than the entire layout.


Templates can load views, but views do not load templates. This separation ensures that templates maintain a consistent page structure while views handle dynamic content.

## Where Templates Are Stored


Templates in Trongate are organized within a dedicated module named `templates`, located in the root directory of your application.

![Directory structure of the 'templates' module](https://trongate.io/docs_pages_pictures/92/templatezep4.png)
    
*The 'templates' directory in a Trongate application*
### The Templates Module


The `templates` directory functions as a standard Trongate module, ensuring global accessibility while maintaining the framework's modular architecture. This module typically includes:


- **controllers/:** Contains `Templates.php`, the controller responsible for loading templates.
- **views/:** Stores the template files that define the structure of web pages.

> [!NOTE]
> **Just To Let You Know...**
>
> In this documentation, the terms **template module** and **template directory** refer to the same entity: the `templates` folder at the root of your Trongate application.


## Design Philosophy


Trongate's approach to templates is guided by the following principles:


- **Stability:** Trongate emphasizes long-term stability, allowing developers to build applications with confidence.
- **Performance:** Templates are designed to minimize overhead, ensuring efficient page rendering.
- **Flexibility:** Trongate provides developers with the freedom to implement custom designs or integrate third-party libraries as needed.

## Independence from Third-Party Dependencies


Trongate does not impose dependencies on external CSS or JavaScript libraries. Unlike some frameworks that are tightly coupled with specific frontend tools (e.g., Bootstrap or Tailwind), Trongate allows developers to choose their preferred technologies. This approach avoids common issues such as dependency conflicts, security vulnerabilities, and design limitations.

## In Summary


Trongate's templating system offers developers a flexible and robust foundation for building web applications. By combining pure PHP with a modular structure, Trongate enables the creation of consistent, reusable templates without imposing unnecessary restrictions. Whether you prefer to build from scratch or integrate third-party tools, Trongate provides the tools and flexibility to meet your needs.

