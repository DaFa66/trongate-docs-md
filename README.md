# Trongate Docs (Markdown) — Converted v1 Documentation

**T**his repository converts the Trongate v1 HTML documentation from the HTML source files into Markdown, making it suitable for LLM integration, RAG, and other AI tools for search indexing, vector databases, as well as GitHub Pages.

---

## Purpose

This project takes the HTML docs from the HTML Trongate docs repository and converts them into readable, well-structured Markdown files so you can:

* Integrate into vector databases for RAG use
* Pull into MCPs like [Context 7](https://context7.com/) or custom MCPs
* Publish the docs as Markdown (GitHub Pages, MkDocs, VuePress, etc.)
* Edit, version, and extend docs in a standard text format
* Integrate with toolchains and CI/CD for documentation automation

---

## What’s included

Converted Markdown files grouped by logical collections (same collection definitions used from the source `docs_collections.json`).

---

## Repo layout (summary)

```
/
├─ php_framework/        # Converted framework guide Markdown
├─ reference/            # API / reference material
├─ trongate_css/         # Styling & CSS docs as Markdown
├─ trongate_mx/          # Our very own HTMX style JavaScript library 
├─ LICENSE
└─ README.md
```

---

## How the conversion works (high level)

1. Input: HTML files from the official HTML docs repo.
2. Grouping: Files are mapped into collections using `docs_collections.json`.

## What's coming next:

1. Transformations into books:

   * Remove numeric prefixes (e.g. `0001-intro.html` → `intro.md`).
   * Normalise headings and fix acronym casing.
   * Add a single book title at the top of each collection and insert the description from `docs_collections.json`.
   * Generate a table of contents (TOC) under the description.
2. Focus on vector database integration for LLM consumption.
3. Output: Clean Markdown files ready for consumption by static doc generators.

> Notes: The conversion emphasizes minimal manual editing after conversion — most changes are automated, but human review is recommended for complex pages (embedded examples, multi-column layouts or interactive content).

---

## Contributing

Contributions welcome:

* Fix conversion edge-cases (tables, code blocks, embedded assets).
* Add CI to convert on push from the upstream HTML docs or provide automated pull requests when upstream docs change.

---

## Status & Roadmap

* ✅ Base conversion for many v1 docs is complete.
* ⚠️ Some pages still need manual cleanup (complex HTML structures, screenshots, or non-standard markup).
* Planned: integrate an automated pipeline to run on updates to the upstream HTML docs.

---

## License

This repository is released under the MIT License. See `LICENSE` for details.

---

## Acknowledgements & References

* The official Trongate landing page and documentation provide the canonical reference material and should be referenced for authoritative guidance.
* The original HTML docs were sourced from the official Trongate docs repository.

---

## Links

* Official website: [https://trongate.io/](https://trongate.io/)
* Official docs landing: [https://trongate.io/documentation](https://trongate.io/documentation)
* Trongate framework repo: [https://github.com/trongate/trongate-framework](https://github.com/trongate/trongate-framework)
* HTML docs (source): [https://github.com/trongate/trongate-docs](https://github.com/trongate/trongate-docs)
* Upcoming Trongate v2 (beta): [https://github.com/trongate/trongate-v2-beta](https://github.com/trongate/trongate-v2-beta)

* All docs as HTML: [https://dafadev.net/a1/tgdocs](https://dafadev.net/a1/tgdocs)
* Automated docs on the Framework using MKDocs: [https://ums.myds.me/tg_docs/](https://ums.myds.me/tg_docs/)
* Automated docs by Dom using doxygen: [https://vtlsoftware.co.uk/trongatedocs/index.html](https://vtlsoftware.co.uk/trongatedocs/index.html)
* This repository: [https://github.com/DaFa66/trongate-docs-md](https://github.com/DaFa66/trongate-docs-md)

---

## Final notes

If you want, I can:

* format these Markdown files for an MkDocs or Docusaurus site,
* add a CI workflow to rebuild Markdown automatically when the upstream HTML docs change,
* or produce a styled landing README that mirrors the official Trongate site aesthetic.
