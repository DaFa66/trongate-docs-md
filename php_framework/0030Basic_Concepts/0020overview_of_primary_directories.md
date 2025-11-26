# Overview of Primary Directories


The Trongate Framework is a structured collection of directories and files designed to streamline the web development process. Below is a concise summary of each directory's purpose.

![The contents of a basic Trongate web application](https://trongate.io/docs/images/21/trongateS9Tm.png)
        
*The contents of a basic Trongate Web Application.*
## The Engine Directory


The **engine** directory contains the core functionality of the Trongate framework, including files responsible for loading classes, handling routes, and providing helper functions. Modifying files within this directory is strongly discouraged unless absolutely necessary and fully understood.

## The Config Directory


The **config** directory stores essential configuration settings for your application, such as the base URL, environment settings, and default controllers. These settings are globally accessible throughout the application.

> [!CAUTION]
> Never deploy a Trongate web application with the "ENV" setting configured to "dev".


## The Modules Directory


The **modules** directory organizes distinct components of the Trongate application, each referred to as a **module**. Modules encapsulate all functionality required for a specific feature, making them self-contained and reusable. Typically, a Trongate module includes the following subdirectories:


- **Controllers:** Handle the business logic of the module.
- **Views:** Manage the presentation layer and user interface elements.
- **Assets:** Store related files such as CSS, JavaScript, and images.

## The Templates Directory


The **templates** directory is used for storing HTML templates. Unlike other frameworks that rely on separate templating engines, Trongate leverages PHP itself as its templating engine. This approach simplifies the learning curve and enhances performance.

## The Public Directory


The **public** directory serves as the primary entry point for a Trongate web application, containing the `index.php` file. It also houses assets such as CSS, JavaScript, and images that are directly served to clients.  Entire HTML themes can also be stored within the public directory.

> [!WARNING]
> The **public** and **engine** directories contain essential license files. These files include specific framework version details and are critical for managing updates via the Trongate Desktop App. Modifying or removing these files may disrupt the update process and should be avoided to maintain system integrity.


