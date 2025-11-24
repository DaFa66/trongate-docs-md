# Code Distribution and Management


Trongate developers can use [Packagist](documentation/display/php_framework/controllers/using-packagist-with-trongate) for sharing code, just as with other PHP frameworks. However, Trongate modules are designed to be entirely self-contained, enabling seamless distribution without reliance on external platforms. This means modules can be copied directly from one project and pasted into another, making them highly portable and easy to integrate.


If a module includes an SQL file, Trongate activates a built-in **Module Import Wizard**. This wizard prompts the user to import SQL code with a single click, ensuring smooth integration of modules that depend on database structures. For more details, see the [Module Import Wizard chapter](documentation/display/php_framework/the-module-import-wizard).

## Self-Contained Modules: A Key Strength


Trongate's modular architecture emphasizes independence and portability. Each module encapsulates all necessary components, including controllers, views, assets, and optional database configurations. This design allows developers to copy and paste modules between projects without additional setup or dependencies. Whether you're reusing modules within a single application or sharing them across multiple projects, the process is straightforward and efficient.

## Trongate's Code Sharing Platform


For developers seeking pre-built modules, Trongate offers "[The Module Market](https://trongate.io/module-market)"—a platform tailored specifically for Trongate modules. While not required for module distribution, The Module Market provides a centralized location for discovering high-quality, open-source modules that meet Trongate's standards for integration and compatibility. Each module is maintained by a single developer, ensuring accountability and consistent quality.

## Comparative Overview of Code Sharing Platforms


The table below compares popular web development technologies, highlighting their approaches to managing and sharing intellectual assets such as code.

| Technology | Platform | Management Model | Security and Stability Focus |
| ---|---|---|---|
| Node.js | NPM (Node Package Manager) | Community-driven; multiple contributors | Dependencies managed by versions; potential security risks from open contributions |
| Ruby on Rails | RubyGems | Community-driven; multiple contributors per gem | Moderate; includes efforts to audit gems but remains open to community contributions |
| Other PHP Frameworks | Packagist | Community-driven; inter-version dependencies allowed | Security audits are less centralized; relies on community vigilance and Composer's dependency management |
| Trongate | Self-contained modules / Module Market | Single point of accountability; one developer responsible per module | Higher security and stability due to developer accountability and controlled updates |
