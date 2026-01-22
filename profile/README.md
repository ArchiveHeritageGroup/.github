# Archive & Heritage Group (AHG)

Archive & Heritage Group (AHG) builds production-grade extensions, integration tooling, and automation around **Access to Memory (AtoM)** to support real archival, records management, and GLAM workflows.

Our engineering focus is a stable base platform that changes rarely, with functionality delivered through modular plugins and supporting SDKs.

## What we build for AtoM

- **atom-framework**: the stable platform layer (database integration, Qubit/Symfony compatibility shims, extension lifecycle management, migrations runner, shared contracts/utilities).
- **atom-ahg-plugins**: AHG-maintained plugins providing functional modules (rights/privacy, provenance, Spectrum workflows, preservation/condition, IIIF/3D, researcher tooling, audit trail, and more).
- **atom-extensions-catalog**: curated catalog and documentation to install, enable, and maintain extensions consistently across environments.

## SDKs and client libraries

We maintain shared client libraries to reduce duplication across plugins and tools:

- **atom-ahg-python**: Python SDK for interacting with AHG/AtoM services and APIs (automation, processing pipelines, integrations).
- **atom-client-js**: TypeScript/JavaScript SDK for reusable UI widgets and a consistent API client layer.

## Repository map

Start here, in this order:

1. **atom-extensions-catalog** — installation guidance, curated list of extensions, and recommended deployment patterns.
2. **atom-framework** — the base platform (intended to remain stable).
3. **atom-ahg-plugins** — functional plugins and modules built on the platform.

## Compatibility targets

- **AtoM**: 2.10.x (primary)
- **PHP**: 8.3
- **Database**: MySQL 8.x
- **Web server**: Nginx (PHP-FPM)

## Contribution model

We welcome community participation and third-party plugin development.

- **Framework**: treated as a stable base; changes are conservative and reviewed by AHG maintainers.
- **Plugins**: the primary contribution surface; new features should be delivered as plugins.
- **Naming**:
  - `ahg<Feature>Plugin` is reserved for AHG-maintained plugins.
  - Third-party plugins should use a vendor prefix: `<vendorPrefix><Feature>Plugin`.

To propose a new plugin for the ecosystem, contribute it in your own repository and submit it for inclusion via the catalog process.

## Security

If you believe you have found a security issue, please use GitHub Security Advisories where available. For operational issues, open an issue in the relevant repository with clear reproduction steps and environment details.

## Links

- Organisation: https://github.com/ArchiveHeritageGroup
- Framework: https://github.com/ArchiveHeritageGroup/atom-framework
- Plugins: https://github.com/ArchiveHeritageGroup/atom-ahg-plugins
- Catalog: https://github.com/ArchiveHeritageGroup/atom-extensions-catalog
