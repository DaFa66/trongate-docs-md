# Additional Considerations


Trongate's File Asset Manager introduces important considerations regarding application architecture. For instance, imagine developing a picture uploader for a 'members' module where members can upload pictures to their profile pages.


For developers building such a feature, the decision of where to store members' pictures becomes crucial. Let's explore two common approaches:


- **Storing Pictures in the Public Directory:** This approach involves placing member pictures directly within the 'public' directory of the application, typically in a subdirectory like 'images' or 'member_pics'.
- **Storing Pictures in the 'Assets' Directory of the 'Members' Module:** Alternatively, developers may choose to store these images within the 'assets' directory of the 'members' module itself.


Here are the pros and cons of each approach:

## Storing Pictures in the 'Public' Directory

### Pros:


- Easily accessible and straightforward to link directly from web pages.
- Reduces the likelihood of 404 errors caused by file or path naming conflicts.
- Facilitates module reusability by maintaining a compact 'members' module size.

### Cons:


- Compromises module encapsulation as assets are dispersed across separate directories.
- Imposes additional responsibility on developers to manage directory naming and access permissions.
- Elevates the risk of unintentional image pollution within the designated directory.

## Storing Pictures in the 'Members' Module

### Pros:


- Enhances module encapsulation by centralizing related assets within the 'members' module.
- Reduces the risk of non-related images coexisting within the image directory.
- Provides granular control over access permissions and asset visibility.

### Cons:


- Requires additional configuration to serve module-specific images through web requests.
- Increases the potential for 404 errors due to conflicting file or path names within the application.
- Possibility of creating overly large modules that are challenging to reuse efficiently.


---

## In Conclusion


Web development often involves making critical decisions about where to store assets like pictures, which are pivotal to an application's architecture and scalability. There is no one-size-fits-all solution, and these choices are integral to the iterative process of web development. Trongate provides developers with flexible tools, encouraging the creation of applications that meet specific needs without imposing rigid methodologies.


Developers are encouraged to embrace these decisions as opportunities to optimize their application's performance and maintainability. It is the responsibility of developers - and not the framework - to determine the most effective architecture structures for *their* specific needs.

> [!TIP]
> **Best Practices**
>
> If developers find themselves pondering questions like "Where should I store x?" or "How should I structure my app?" - rest assured, these are common considerations in web development. The decision-making process should be guided by factors such as the specific requirements of the application, potential reuse of the module across different applications, whether there are plans to list the module on the [Trongate Module Market](https://trongate.io/module-market), and the anticipated file size implications of choosing option 'A' versus option 'B'.


