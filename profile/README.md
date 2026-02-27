# Archive & Heritage Group (AHG)

Archive & Heritage Group (AHG) builds production-grade extensions, integration tooling, and automation around **Access to Memory (AtoM)** to support archival, records management, and GLAM workflows.

Our engineering model is intentionally modular:

- **atom-framework** is the stable base and changes rarely.
- **Plugins** deliver almost all functional capability.
- **Shared SDKs** prevent duplicated client logic across UI modules and automation tooling.
- **atom-extensions-catalog** is the canonical entry point for documentation and installation patterns.

---

## Start here

1. **atom-extensions-catalog**
   Documentation, catalog and manifest, install and upgrade patterns, compatibility guidance.

2. **atom-framework**
   Stable base platform: extension lifecycle, migrations runner, DB bootstrap, Qubit compatibility shims, contracts and utilities.

3. **atom-ahg-plugins**
   AHG-maintained plugins: rights, privacy, provenance, Spectrum and loans, preservation and condition, IIIF and 3D, research and search, engagement modules.

4. **[Product Roadmap](https://github.com/ArchiveHeritageGroup/atom-extensions-catalog/blob/main/ROADMAP.md)**
   What's completed, in progress, planned, and future — with competitive context.

---

## Architecture overview

### Core principles

- The **framework** provides infrastructure and contracts.
- **Plugins** implement domain features, workflows, and UI.
- **SDKs** provide shared API clients and UI building blocks.
- The **catalog** documents what is supported and how to deploy it.

### Full stack diagram

```mermaid

%%{init: {"flowchart":{"nodeSpacing":55,"rankSpacing":65}}}%%
flowchart TB

  FW[atom-framework stable base]

  subgraph SDK["Shared SDKs"]
    JS[atom-client-js]
    PY[atom-ahg-python]
  end

  subgraph GOV["Catalog"]
    CAT[atom-extensions-catalog]
  end

  subgraph UI["UI and Presentation"]
    THEME[ahgThemeB5Plugin]
    DISP[ahgDisplayPlugin]
    GALL[ahgGalleryPlugin]
    IIIF[ahgIiifCollectionPlugin]
    M3D[ahg3DModelPlugin]
  end

  subgraph SEC["Security Rights Privacy Access"]
    CLR[ahgSecurityClearancePlugin]
    RGT[ahgRightsPlugin]
    XRGT[ahgExtendedRightsPlugin]
    PRV[ahgPrivacyPlugin]
    ARQ[ahgAccessRequestPlugin]
    PUB[ahgRequestToPublishPlugin]
  end

  subgraph GOV2["Provenance Audit Governance"]
    PROV[ahgProvenancePlugin]
    AUD[ahgAuditTrailPlugin]
    DON[ahgDonorAgreementPlugin]
  end

  subgraph SECTOR["Sector Workflows"]
    SPEC[ahgSpectrumPlugin]
    LOAN[ahgLoanPlugin]
    MUS[ahgMuseumPlugin]
    LIB[ahgLibraryPlugin]
    ACC[ahgHeritageAccountingPlugin]
  end

  subgraph PRES["Preservation and Digital Assets"]
    PPR[ahgPreservationPlugin]
    COND[ahgConditionPlugin]
    DAM[ahgDAMPlugin]
  end

  subgraph AI["AI Search Research Reporting"]
    NER[ahgAIPlugin]
    DISC[ahgDiscoveryPlugin]
    META[ahgMetadataExtractionPlugin]
    SEM[ahgSemanticSearchPlugin]
    RSR[ahgResearchPlugin]
    RIC[ahgRicExplorerPlugin]
    REP[ahgReportBuilderPlugin]
  end

  subgraph ENG["User Engagement"]
    FAV[ahgFavoritesPlugin]
    FDB[ahgFeedbackPlugin]
    CART[ahgCartPlugin]
  end

  subgraph OPS["Operations Integration Migration"]
    API[ahgAPIPlugin]
    GQL[ahgGraphQLPlugin]
    BAK[ahgBackupPlugin]
    DMIG[ahgDataMigrationPlugin]
    MIG[ahgMigrationPlugin]
    VEND[ahgVendorPlugin]
  end

  FW --> UI
  FW --> SEC
  FW --> GOV2
  FW --> SECTOR
  FW --> PRES
  FW --> AI
  FW --> ENG
  FW --> OPS

  CAT --> FW
  JS --> UI
  PY --> OPS

```

---

## Repository map

**atom-extensions-catalog** — Canonical documentation and recommended deployment patterns. Catalog and manifest approach for consistent installs and upgrades. Governance entry point for community contributions (plugin registration).

**atom-framework** — Stable base platform intended to change rarely: DB bootstrap and connection ownership, extension lifecycle management (install, enable, disable, dependencies, core and locked), generic migrations runner, Qubit compatibility layer and shims, shared contracts and utilities.

**atom-ahg-plugins** — AHG-maintained plugins providing feature modules: Rights, privacy, and security clearance. Provenance, audit trail, and governance workflows. Spectrum procedures and loan workflows. Preservation, condition, DAM, and display. IIIF and 3D support. AI enrichment, semantic search, research tooling. User engagement modules.

**atom-client-js** — Shared TypeScript library: API client patterns for UI modules, reusable UI widgets and components, consistent handling of authentication, pagination, retries, and error reporting.

**atom-ahg-python** — Shared Python library: API client patterns for automation and integration tooling, consistent auth, pagination, batching, retries. Useful for ETL, migration tooling, processing pipelines, and scheduled jobs.

---

## Compatibility targets

- **AtoM:** 2.10.x
- **PHP:** 8.3
- **Database:** MySQL 8.x
- **Web server:** Nginx with PHP-FPM
- **Search:** Elasticsearch 7.x
- **Vector store:** Qdrant (optional — for semantic search)
- **AI backend:** Ollama / spaCy / Argos Translate (optional — for AI features)

---

## Plugin map by capability

```mermaid
%%{init: {"flowchart":{"nodeSpacing":60,"rankSpacing":70}}}%%
flowchart TB

  subgraph L1["Lane 1 Clients"]
    USERS[Users]
    BROWSER[Browser UI]
    AUTO[Automation and Tools]
  end

  subgraph L2["Lane 2 SDKs"]
    JS[atom-client-js]
    PY[atom-ahg-python]
  end

  subgraph L3["Lane 3 AtoM runtime"]
    PLUGINS[AHG plugins]
    ATOM[AtoM 2.10.x runtime]
  end

  subgraph L4["Lane 4 Framework base"]
    FW[atom-framework]
    EXT[Extension lifecycle]
    MIG[Migrations runner]
    DBB[Database bootstrap]
    COMP[Compatibility shims]
    CTR[Contracts]
    UTIL[Shared utilities]
  end

  subgraph L5["Lane 5 Data stores"]
    MYSQL[(MySQL)]
    ES[(Elasticsearch)]
    QD[(Qdrant)]
    FS[(Storage)]
  end

  subgraph L6["Lane 6 Catalog and governance"]
    CAT[atom-extensions-catalog]
  end

  USERS --> BROWSER --> PLUGINS --> ATOM
  AUTO --> PY
  BROWSER --> JS

  PLUGINS --> FW
  FW --> EXT
  FW --> MIG
  FW --> DBB
  FW --> COMP
  FW --> CTR
  FW --> UTIL

  ATOM --> MYSQL
  ATOM --> ES
  PLUGINS --> QD
  PLUGINS --> FS
  UTIL --> FS
  DBB --> MYSQL

  CAT --> EXT
  JS --> PLUGINS
  PY --> FW

```

---

## Contribution model

**What to contribute** — New features should be delivered as plugins. The framework is treated as stable base infrastructure and changes are conservative.

**Naming conventions** — Prefix `ahg` is reserved for AHG-maintained plugins. Third parties must use a vendor prefix: `<vendorPrefix><Feature>Plugin`. `machine_name` must match folder name and configuration class prefix. `extension.json` is required and authoritative for version and dependencies.

**Security** — For security issues, use GitHub Security Advisories where enabled. For operational issues, open an issue in the relevant repository with environment details and reproduction steps.

---

**Contact:** [The Archive and Heritage Group](https://theahg.co.za)
**License:** GPL-3.0
