# The Archive and Heritage Digital Commons Group (AHG)

AHG builds open-source software for archives, museums, libraries and records managers. There are three lines of work, and they are kept deliberately separate: **Heratio**, our own GLAM platform; **AHG Extensions for AtoM**, for institutions that want to stay on Access to Memory; and **OpenRiC**, an open specification for exchanging archival description built on the ICA's Records in Contexts.

## Heratio

[Heratio](https://heratio.org) is a self-hostable GLAM platform on Laravel 12: archival description, museum collections management, digital asset management and records management in one application. It is Records in Contexts native and supports ISAD(G), ISAAR(CPF) and ISDIAH, Spectrum procedures, OAIS/OCFL preservation and IIIF. Country-specific compliance is added through pluggable modules rather than built into the core.

Source: [heratio](https://github.com/ArchiveHeritageGroup/heratio) (AGPL-3.0). Releases are published on the repository's [releases page](https://github.com/ArchiveHeritageGroup/heratio/releases).

## AHG Extensions for AtoM

For institutions running [Access to Memory](https://www.accesstomemory.org) 2.10, the extensions add preservation, provenance, Records in Contexts, AI-assisted discovery, museum, library and DAM workflows, rights, privacy and governance. It is not a fork: AtoM stays as upstream ships it, and each capability is a plugin an institution can install or leave out. The extensions are a separate product from Heratio.

| Repository | What it is |
| --- | --- |
| [atom-ahg-plugins](https://github.com/ArchiveHeritageGroup/atom-ahg-plugins) | The plugins and themes, with packaged downloads (AGPL-3.0) |
| [atom-framework](https://github.com/ArchiveHeritageGroup/atom-framework) | The framework layer the plugins run on: query builder and extension manager for AtoM 2.8-2.10 (AGPL-3.0) |
| [atom-extensions-catalog](https://github.com/ArchiveHeritageGroup/atom-extensions-catalog) | The catalogue: what each extension does, how to install and upgrade, and compatibility |

## OpenRiC

[OpenRiC](https://openric.org) is an open, implementation-neutral specification for publishing and exchanging archival description built on RiC-CM 1.0 and RiC-O 1.1. It defines a testable HTTP contract (profiles, JSON Schemas, SHACL shapes, fixtures, an OpenAPI contract and a conformance probe) so that records, people, activities, places and their relationships can move between archival systems. Any system can implement it, and it does not depend on any AHG product. The [OpenRiC](https://github.com/ArchiveHeritageGroup/OpenRiC) repository here is a signpost: the specification itself lives in the [openric](https://github.com/openric) organisation.

## Tools

| Repository | What it is |
| --- | --- |
| [ahg-archives-mcp](https://github.com/ArchiveHeritageGroup/ahg-archives-mcp) | An MCP server that lets an AI assistant search and read archival catalogues (stock AtoM, AtoM with the AHG Extensions, Heratio and OpenRiC) and propose improvements. Nothing changes until an archivist approves it. In development (AGPL-3.0) |
| [inference-receipts](https://github.com/ArchiveHeritageGroup/inference-receipts) | A tamper-evident chain of receipts for AI inference calls (RFC 8785 JSON canonicalisation and Ed25519 signatures), aligned with EU AI Act Article 12. Pure PHP with no framework dependencies (Apache-2.0) |

The earlier AtoM API SDKs, [atom-client-js](https://github.com/ArchiveHeritageGroup/atom-client-js) and [atom-ahg-python](https://github.com/ArchiveHeritageGroup/atom-ahg-python), are retired and archived.

## Contact

Website: [theahg.co.za](https://theahg.co.za). For bugs or questions about a product, open an issue in its repository, with your environment and the steps to reproduce. Report security issues privately through GitHub Security Advisories where a repository has them enabled, not in a public issue.

Licences differ by repository, so check each repository's own licence file.
