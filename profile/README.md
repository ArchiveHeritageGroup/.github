# Archive & Heritage Group (AHG)

We build production-grade extensions, integration tooling, and automation around **Access to Memory (AtoM)** for archival and GLAM workflows.  
Our engineering model: a stable base **framework** that changes rarely, with functionality delivered via modular **plugins** and shared **SDKs**.

## Start here

1. **atom-extensions-catalog** — documentation, catalog/manifest, install/upgrade guidance  
2. **atom-framework** — stable base platform (extension lifecycle, migrations, DB bootstrap, Qubit/Symfony compatibility)  
3. **atom-ahg-plugins** — AHG plugins (rights/privacy, provenance, Spectrum/loans, preservation/condition, IIIF/3D, search/research, user engagement)

## Architecture
## Architecture

```mermaid
flowchart TB
  subgraph Clients
    U[Archivists / Researchers]
    B[Browser UI]
  end

  subgraph AtoM["AtoM 2.10.x (Symfony/Qubit)"]
    Q[Qubit Domain Model + Symfony 1.x]
    P[AHG Plugins (Symfony plugins)]
  end

  subgraph FW["AHG Framework (atom-framework) — stable base"]
    DBB[DB bootstrap / connection ownership]
    MIG[Migrations runner]
    EXT[Extension lifecycle manager<br/>(install/enable/disable/deps)]
    COMP[Qubit compatibility/shims]
    CTR[Contracts/Interfaces]
    UTIL[Shared utilities]
  end

  subgraph SDK["Shared SDKs"]
    JS[atom-client-js<br/>(TS API client + UI widgets)]
    PY[atom-ahg-python<br/>(Python API client)]
  end

  subgraph Data["Data Stores / Services"]
    MYSQL[(MySQL 8)]
    ES[(Elasticsearch)]
    FS[(Filesystem / Object storage)]
  end

  U --> B --> P --> Q
  P --> FW
  FW --> MYSQL
  Q --> MYSQL
  Q --> ES
  P --> FS
  FW --> FS

  JS --> P
  PY --> FW

  subgraph GOV["Catalog / Governance"]
    CAT[atom-extensions-catalog<br/>(manifest + docs)]
  end
  CAT --> EXT


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
