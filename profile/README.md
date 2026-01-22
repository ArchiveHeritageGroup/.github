# Archive & Heritage Group (AHG)

We build production-grade extensions, integration tooling, and automation around **Access to Memory (AtoM)** for archival and GLAM workflows.  
Our engineering model: a stable base **framework** that changes rarely, with functionality delivered via modular **plugins** and shared **SDKs**.

## Start here

1. **atom-extensions-catalog** — documentation, catalog/manifest, install/upgrade guidance  
2. **atom-framework** — stable base platform (extension lifecycle, migrations, DB bootstrap, Qubit/Symfony compatibility)  
3. **atom-ahg-plugins** — AHG plugins (rights/privacy, provenance, Spectrum/loans, preservation/condition, IIIF/3D, search/research, user engagement)

## Architecture

- **Framework (stable)**: DB bootstrap + Qubit replacements/shims + extension lifecycle + migrations runner + contracts
- **Plugins (feature surface)**: UI + workflows + domain rules + optional services
- **SDKs (shared clients)**:
  - **atom-client-js**: TypeScript client + reusable UI components/widgets
  - **atom-ahg-python**: Python client SDK for automation/processing pipelines and integrations

## Compatibility targets

- **AtoM**: 2.10.x (primary)
- **PHP**: 8.3
- **Database**: MySQL 8.x
- **Web server**: Nginx (PHP-FPM)

## Contribution model

- **Framework**: conservative changes, reviewed by AHG maintainers (platform stability)
- **Plugins**: primary contribution surface; new features ship as plugins
- **Naming**:
  - `ahg<Feature>Plugin` reserved for AHG-maintained plugins
  - Third parties use `<vendorPrefix><Feature>Plugin`

## Security

Use GitHub Security Advisories where available. For operational issues, open an issue in the relevant repository with environment details and reproduction steps.

## Repository map

- atom-extensions-catalog — catalog + documentation + governance
- atom-framework — stable base
- atom-ahg-plugins — plugins bundle (AHG)
- atom-client-js — TS SDK
- atom-ahg-python — Python SDK
