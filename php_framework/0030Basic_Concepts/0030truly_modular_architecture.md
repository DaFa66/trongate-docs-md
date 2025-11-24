# Truly Modular Architecture


Trongate applications exemplify a **truly modular** architecture, setting them apart from traditional PHP frameworks that often rely on pseudo-modularity and intricate dependencies. Unlike frameworks that depend on a 'vendor' directory managed by Composer for library loading, Trongate directly and independently loads modules. This efficient design minimizes overhead, streamlines the initialization process, and delivers significant performance improvements, as validated by independent benchmarks.

> [!NOTE]
> **Just To Let You Know...**
>
> Modularity in software design involves breaking down a system into independent, interchangeable modules. Each module encapsulates specific functionality, helping manage complexity, improve reusability, and enhance maintainability.


## Understanding the Modules Directory


In the Trongate framework, the majority of developer-authored code resides within the "modules" directory. This directory implements Trongate's HAVC (Hierarchical Assets View Controller) architectural pattern, which enhances modularity and promotes clean, organized code.

### What Is HAVC?


For developers familiar with the traditional MVC pattern, HAVC will feel intuitive. It retains core MVC components, such as controller files for application logic and views for presentation layers.


In Trongate, each module within the modules directory functions as an independent MVC cluster. These modules are self-contained but can interact with other modules and parts of the broader application. Additionally, HAVC supports the inclusion of **modules within modules**, offering enhanced modularity and flexibility to design scalable, maintainable applications.


The graphic below illustrates the typical structure of the modules directory. The two-way arrows indicate bidirectional communication between modules, allowing them to exchange information with both controller and view files.

![Diagram of Trongate Modules Directory](images/25/havcuSkk.png)
        
*A Visual Representation of Hierarchical Assets View Controller Architecture.*
## HAVC vs. HMVC


Trongate's modular architecture shares conceptual similarities with HMVC by introducing hierarchy through submodules within modules. However, Trongate's structure is more flexible and less rigid than the strict hierarchical design typical of HMVC. This flexibility allows Trongate to combine structured code organization with loosely coupled systems, providing developers with adaptability and efficiency. As a result, Trongate excels in delivering robust, straightforward solutions without the complex dependencies often associated with traditional HMVC frameworks.

