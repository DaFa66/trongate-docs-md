# The Anatomy of a Trongate Module


A Trongate module is typically organized into three primary directories, each serving a distinct purpose:


- **Controllers:** This directory contains the business logic of the module. It typically includes one or more PHP files, with at least one file defining a PHP class. While most modules contain a single PHP class file, some may require multiple files depending on complexity.
- **Views:** The views directory houses presentational content, primarily HTML. These PHP files are designed to integrate seamlessly with HTML, focusing on the user interface rather than business logic. This directory is optional, as not all modules produce presentational output.
- **Assets:** This directory stores additional resources such as CSS, JavaScript, images, and configuration files for API endpoints. Like the views directory, this is optional and only included when necessary.

![The basic structure of a typical Trongate module](https://trongate.io/images/65/trongate7MEL.png)
        
*The basic structure of a typical Trongate module.*
> [!NOTE]
> **Just To Let You Know...**
>
> ### What About the 'Models' Directory?
> 
> 
> To facilitate secure and efficient database interactions, all Trongate modules can utilize a centralized 'Model' PHP class. This class resides within the Trongate framework's 'engine' directory, rather than within individual modules. Centralizing the model simplifies maintenance, enhances security, and ensures consistent database interactions across all modules.
> 
> 
> For more information regarding Trongate's [Model class](documentation-ref/list_refs/class_reference/the-model-class), please refer to the [Database Operations](documentation/display/php_framework/database-operations) chapter.


