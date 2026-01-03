# Trongate v1 - Documentation (Markdown)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Trongate](https://img.shields.io/badge/Trongate-grey.svg)](https://trongate.io)
[![Trongate](https://img.shields.io/badge/Framework-v1-purple.svg)](https://github.com/trongate/trongate-framework)
[![Trongate](https://img.shields.io/badge/html-v1-green.svg)](https://github.com/trongate/trongate-docs)
[![Documentation](https://img.shields.io/badge/docs-markdown-orange.svg)](https://github.com/DaFa66/trongate-docs-md)

> **LLM-friendly Markdown conversion of the official Trongate v1 HTML documentation**

This repository provides the complete Trongate v1 documentation converted from HTML to clean, well-structured Markdown format. Designed for seamless integration with AI tools, vector databases, static site generators, and modern documentation workflows.

> [!IMPORTANT]
> **Trongate v2 is coming!** Scheduled launch: **6th January 2026** (subject to confirmation). The new version will feature revamped documentation. [Explore the beta →](https://github.com/trongate/Trongate-v2-Dev)

---

## 📋 Table of Contents

- [Overview](#-overview)
- [What's Coming: Trongate v2](#-whats-coming-trongate-v2)
- [Features](#-features)
- [Repository Structure](#-repository-structure)
- [Getting Started](#-getting-started)
- [Use Cases](#-use-cases)
- [Conversion Process](#-conversion-process)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [Status](#-status)
- [Resources](#-resources)
- [License](#-license)

---

## 🎯 Overview

The Trongate framework's official documentation is maintained in HTML format. This project converts those HTML files into Markdown, making the documentation more accessible for:

- **AI/LLM Integration**: RAG (Retrieval-Augmented Generation) systems, vector databases, and semantic search
- **Documentation Platforms**: GitHub Pages, MkDocs, Docusaurus, VuePress, and other static site generators
- **Version Control**: Track documentation changes with standard diff tools
- **Automation**: CI/CD pipelines and automated documentation workflows
- **Custom Tooling**: MCPs, search indexing, and custom documentation systems

**Note**: This repository focuses on Trongate v1 documentation. Trongate v2 with revamped documentation is scheduled for release in early 2026.

---

## 🚀 What's Coming: Trongate v2

**Trongate v2 is going to be a winner!**

Trongate v2 represents a revolutionary leap forward with groundbreaking architectural changes and a completely revamped documentation experience. Confirmed launch date: **Tuesday, 6th January 2026**.

### 🎯 Major Highlights

#### **Dramatic Engine Size Reduction**

- **v1 Engine**: ~5,530 lines of code
- **v2 Engine**: ~2,320 lines of code
- **Result**: 58% reduction in core framework size!

#### **Module-First Architecture**

Almost everything becomes a module:

- Templates → Module
- Database (DB) → Module
- Validation → Module
- Image → Module
- File → Module

This radical simplification means:

- Faster framework performance
- Easier to understand and customise
- AI engines can easily comprehend the entire framework
- Community can build specialised modules (e.g., `validation_japan` for Japanese form validation)

#### **Built-in Internationalisation**

Creating multilingual sites with localised validation messages becomes a **3-minute task**. Perfect for global applications!

#### **Trongate MX Included**

The powerful HTMX-style JavaScript library will be included by default (but is optional to use).

#### **AI-Optimised Design**

With the tiny engine size, fully automated AI-driven web development becomes feasible. The framework is being designed for the AI era.

#### **Hyper-Optimised Performance**

Extensive refactoring and optimisation work have produced remarkable results:

**Benchmark Results** (Apache Bench: 1000 requests, 100 concurrent):

- Test #1: 1,417.03 req/sec
- Test #2: 1,908.98 req/sec
- Test #3: 2,192.38 req/sec
- **Average: ~77% performance improvement over v1** 🚀

> [!NOTE]
> These benchmarks were conducted on a **Windows 11** system with **PHP 8.4** and **Apache 2.4**. Results may vary based on your specific environment.

![TGv2](https://drive.google.com/file/d/1S7cKtB1OsktCgsmR-1VAKsz9b5ZBeIMv/view?usp=sharing)

**Core Optimisations:**

- Streamlined autoloader with single filesystem operation
- Regex-based custom route matching with static caching (5-10x faster route resolution)
- Optimised `get_segments()` function (20-30% faster URL parsing)
- Eliminated double controller instantiation (30-50% faster controller loading)
- Explicit lazy-loading for framework classes (40-60% faster property access)
- Priority-based view path resolution (20-30% faster view rendering)

**Overall Impact:**

- 25-40% reduction in framework overhead
- 15-25% improvement for simple pages
- 25-40% improvement for complex pages
- 30-50% improvement under high-traffic scenarios

> [!NOTE]
> These optimisations were achieved while maintaining backward compatibility and the familiar Trongate development experience.

### 💬 What the Community is Saying

> _"The current Trongate is wonderful and easy to use. The flexible becomes even more flexible. And not only is it not at the expense of a slower system, but it speeds things up. Superb!"_ — r-evo

> _"Being able to customise/translate validation messages is going to be a huge plus, especially for non-English web applications."_ — Balazs

> _"Other frameworks are becoming increasingly complex, but Trongate is simplifying, speeding up and becoming more efficient than ever before."_ — Balazs

### 📚 What This Means for This Repository

Once Trongate v2 documentation is released, we plan to:

- Create a parallel conversion for v2 documentation
- Maintain v1 documentation for legacy projects
- Provide clear versioning and migration guides
- Continue supporting both versions during the transition period
- Leverage the new modular architecture for better documentation organisation

> [!TIP]
> Want to get a head start? Check out the [Trongate v2 beta repository](https://github.com/trongate/Trongate-v2-Dev) to explore what's coming! You can also watch the framework being rebuilt live on the [Trongate YouTube channel](https://www.youtube.com/@GlasgowEqualizer).

---

## ✨ Features

- **Complete Coverage**: All major Trongate v1 documentation sections converted
- **Structured Collections**: Organised by logical groupings matching the official documentation structure
- **Clean Formatting**: Proper heading hierarchy, code blocks, and markdown conventions
- **LLM-Optimised**: Formatted for optimal consumption by language models and AI tools
- **Automated Conversion**: Minimal manual intervention required post-conversion
- **Extensible**: Easy to integrate into existing documentation workflows

---

## 📁 Repository Structure

```
trongate-docs-md/
├── php_framework/     # Core PHP framework documentation
├── reference/         # API reference and technical specifications
├── trongate_css/      # CSS framework and styling documentation
├── trongate_mx/       # Trongate MX (HTMX-style) JavaScript library docs
├── LICENSE            # MIT License
└── README.md          # This file
```

Each directory contains converted Markdown files organised by topic, maintaining the same logical structure as the official documentation.

---

## 🚀 Getting Started

### Prerequisites

- Git for cloning the repository
- A Markdown viewer or editor (VS Code, Obsidian, Typora, etc.)
- Optional: Static site generator (MkDocs, Docusaurus) for publishing

### Installation

```bash
# Clone the repository
git clone https://github.com/DaFa66/trongate-docs-md.git

# Navigate to the directory
cd trongate-docs-md

# Browse the documentation
ls -la
```

### Usage

**For Reading:**

- Open any `.md` file in your preferred Markdown viewer
- Navigate through directories to find specific topics

**For Integration:**

- Import into your vector database for RAG applications
- Use with MCP servers like [Context 7](https://context7.com/)
- Build a static site with your preferred generator
- Index for search functionality

**For Development:**

- Reference while building Trongate applications
- Integrate into IDE documentation systems
- Use for offline development reference

---

## 💡 Use Cases

### AI & Machine Learning

- **Vector Databases**: Embed documentation for semantic search and RAG systems
- **LLM Context**: Provide framework knowledge to AI coding assistants
- **Training Data**: Use as training material for Trongate-specific models

### Documentation Publishing

- **Static Sites**: Deploy with MkDocs, Docusaurus, or VuePress
- **GitHub Pages**: Publish directly from this repository
- **Custom Platforms**: Integrate with any Markdown-based documentation system

### Development Workflows

- **Offline Reference**: Access documentation without internet connection
- **IDE Integration**: Link documentation directly in your development environment
- **Version Tracking**: Monitor documentation changes alongside code

---

## 🔄 Conversion Process

The conversion pipeline follows these steps:

1. **Source Extraction**: HTML files retrieved from the [Trongate docs repository](https://github.com/trongate/trongate-docs)
2. **Collection Mapping**: Files organised using `docs_collections.json` structure
3. **HTML to Markdown**: Automated conversion with custom transformations for:
   - Code blocks and syntax highlighting
   - Alert boxes and callouts
   - Tables and lists
   - Images and embedded media
   - Internal and external links
4. **Post-Processing**:
   - Heading normalisation
   - Acronym casing corrections
   - Link validation
   - Formatting consistency checks
5. **Quality Review**: Manual verification of complex pages

> [!NOTE]
> The conversion emphasises automation with minimal manual editing. However, complex pages with multi-column layouts, interactive content, or embedded examples may require human review for optimal results.

---

## 🗺️ Roadmap

### Planned Features

- [ ] **Book Format Transformation**

  - Remove numeric prefixes from filenames (e.g., `0001-intro.html` → `intro.md`)
  - Add collection titles and descriptions from `docs_collections.json`
  - Generate automatic table of contents for each collection
  - Improve heading hierarchy and structure

- [ ] **Enhanced LLM Integration**

  - Optimise chunking for vector databases
  - Add metadata frontmatter for better indexing
  - Create embeddings-friendly formatting

- [ ] **Automation & CI/CD**

  - Automated conversion pipeline on upstream HTML changes
  - Pull request generation for documentation updates
  - Continuous integration testing for conversion quality

- [ ] **Publishing Templates**
  - Pre-configured MkDocs setup
  - Docusaurus theme and configuration
  - GitHub Pages deployment workflow

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

### Areas for Contribution

- **Conversion Improvements**: Fix edge cases in tables, code blocks, or embedded assets
- **Automation**: Build CI/CD pipelines for automatic conversion
- **Documentation**: Improve this README or add usage examples
- **Quality Assurance**: Review converted files and report issues
- **Tooling**: Create scripts for validation, formatting, or publishing

### How to Contribute

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Make your changes
4. Test thoroughly
5. Commit with clear messages (`git commit -m 'Fix: table conversion in API reference'`)
6. Push to your fork (`git push origin feature/improvement`)
7. Open a Pull Request

---

## 📊 Status

| Component          | Status         | Notes                        |
| ------------------ | -------------- | ---------------------------- |
| PHP Framework Docs | ✅ Complete    | Base conversion finished     |
| API Reference      | ✅ Complete    | Base conversion finished     |
| Trongate CSS       | ✅ Complete    | Base conversion finished     |
| Trongate MX        | ✅ Complete    | Base conversion finished     |
| Manual Cleanup     | ⚠️ In Progress | Complex pages need review    |
| Automated Pipeline | 🔄 Planned     | Scheduled for future release |

> [!WARNING]
> Some pages with complex HTML structures, screenshots, or non-standard markup may still require manual cleanup. Please report any formatting issues you encounter.

---

## 🔗 Resources

### Official Trongate Resources

- **Website**: [trongate.io](https://trongate.io/)
- **Official Documentation**: [trongate.io/documentation](https://trongate.io/documentation)
- **Framework Repository**: [github.com/trongate/trongate-framework](https://github.com/trongate/trongate-framework)
- **HTML Docs Source**: [github.com/trongate/trongate-docs](https://github.com/trongate/trongate-docs)
- **Trongate v2 Beta**: [github.com/trongate/Trongate-v2-Dev](https://github.com/trongate/Trongate-v2-Dev)

### Community Documentation Projects

- **HTML Docs Viewer**: [dafadev.net/a1/tgdocs](https://dafadev.net/a1/tgdocs)
- **MkDocs Implementation**: [ums.myds.me/tg_docs/](https://ums.myds.me/tg_docs/)
- **Doxygen Documentation**: [vtlsoftware.co.uk/trongatedocs/](https://vtlsoftware.co.uk/trongatedocs/index.html)

### This Project

- **Repository**: [github.com/DaFa66/trongate-docs-md](https://github.com/DaFa66/trongate-docs-md)
- **Issues**: [Report bugs or request features](https://github.com/DaFa66/trongate-docs-md/issues)

---

## 📄 License

This repository is released under the **MIT License**. See [LICENSE](LICENSE) for full details.

The original Trongate documentation and framework are subject to their own licensing terms. Please refer to the [official Trongate repository](https://github.com/trongate/trongate-framework) for more information.

---

## 🙏 Acknowledgements

- **Trongate Team**: For creating and maintaining the excellent framework and documentation
- **Community Contributors**: For feedback, bug reports, and improvements
- **Original HTML Docs**: Sourced from the [Trongate docs repository](https://github.com/trongate/trongate-docs)

---

<div align="center">

**Questions or suggestions?** [Open an issue](https://github.com/DaFa66/trongate-docs-md/issues) or contribute to the project!

Made with ❤️ for the Trongate community

</div>
