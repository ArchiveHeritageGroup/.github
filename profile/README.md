# Archive & Heritage Group (AHG)

Archive & Heritage Group (AHG) builds production-grade extensions, integration tooling, and automation around **Access to Memory (AtoM)** to support real archival, records management, and GLAM workflows.

Our engineering model is intentionally modular:

- **atom-framework** is the stable base (changes rarely).
- **Plugins** deliver almost all functional capability.
- **Shared SDKs** prevent duplicated client logic across UI modules and automation tooling.
- **atom-extensions-catalog** is the canonical “Start Here” entry point (docs + catalog/manifest).

---

## Start here

1. **ArchiveHeritageGroup/atom-extensions-catalog**  
   Documentation, catalog/manifest, install/upgrade patterns, compatibility guidance.

2. **ArchiveHeritageGroup/atom-framework**  
   Stable base: extension lifecycle, migrations runner, DB bootstrap, compatibility/shims, contracts/utilities.

3. **ArchiveHeritageGroup/atom-ahg-plugins**  
   AHG-maintained plugins: rights/privacy, provenance, Spectrum/loans, preservation/condition, IIIF/3D, research/search, engagement modules.

---

## Architecture

> Principle: the framework provides infrastructure and contracts; plugins implement features.

```mermaid
flowchart TB
  %% Clients
  subgraph Clients
    U[Archivists / Researchers / Administrators]
    B[Browser UI]
    A[Automation / Integrations]
  end

  %% AtoM core
  subgraph AtoM["AtoM 2.10.x (Symfony/Qubit)"]
    Q[Qubit domain + Symfony runtime]
    P[AHG Plugins (Symfony plugins)]
  end

  %% Framework base
  subgraph FW["AHG Framework (atom-framework) — stable base"]
    DBB[DB bootstrap / connection ownership]
    MIG[Migrations runner (generic)]
    EXT[Extension lifecycle manager<br/>(install/enable/disable/deps/core/locked)]
    COMP[Compatibility & shims<br/>(Qubit/Symfony integration points)]
    CTR[Contracts / Interfaces]
    UTIL[Shared utilities<br/>(FS/HTTP/logging/helpers)]
  end

  %% SDKs
  subgraph SDK["Shared SDKs"]
    JS[atom-client-js<br/>(TypeScript client + reusable UI widgets)]
    PY[atom-ahg-python<br/>(Python client SDK for automation/tools)]
  end

  %% Data stores / services
  subgraph Data["Data stores & services"]
    MYSQL[(MySQL 8)]
    ES[(Elasticsearch)]
    FS[(Filesystem / storage)]
  end

  %% Governance
  subgraph GOV["Catalog / Governance"]
    CAT[atom-extensions-catalog<br/>(manifest + docs + install guidance)]
  end

  %% Flows
  U --> B --> P --> Q
  A --> PY
  B --> JS

  P --> FW
  FW --> MYSQL
  Q --> MYSQL
  Q --> ES
  P --> FS
  FW --> FS

  CAT --> EXT
  JS --> P
  PY --> FW


Repository map

ArchiveHeritageGroup/atom-framework
Stable base platform: DB bootstrap, extension lifecycle, migrations runner, compatibility/shims, contracts/utilities.

ArchiveHeritageGroup/atom-ahg-plugins
AHG plugin bundle (feature modules). Vendors should not contribute here unless explicitly invited.

ArchiveHeritageGroup/atom-extensions-catalog
Catalog/manifest + documentation + recommended install/upgrade patterns.

ArchiveHeritageGroup/atom-client-js
Shared JS/TS client: common API client + reusable UI components/widgets.

ArchiveHeritageGroup/atom-ahg-python
Shared Python client: automation/integration tooling client for AHG/AtoM services/APIs.

Compatibility targets

AtoM: 2.10.x (primary)

PHP: 8.3

Database: MySQL 8.x

Web server: Nginx (PHP-FPM)

Search: Elasticsearch (per AtoM deployment requirements)

Plugin catalog (AHG)

Notes:

The list below reflects functional intent implied by plugin naming and module structure.

The framework should not contain feature modules long-term; features belong in plugins.

Security, privacy, rights, access control

ahgSecurityClearancePlugin
Security classifications/clearance rules; embargo/restrictions; audit/security review utilities.

ahgPrivacyPlugin
Privacy controls and policy-driven visibility; privacy workflows (e.g., sensitive field handling, redaction coordination).

ahgRightsPlugin
Rights statements, usage/reuse constraints, rights metadata capture and display.

ahgExtendedRightsPlugin
Extended rights models and workflows beyond baseline rights statements (integrates with clearance/privacy patterns).

ahgAccessRequestPlugin
Access request workflow: request/approve/track access to restricted descriptions/digital objects.

ahgRequestToPublishPlugin
Publication request workflow: review/approval pipeline for controlled publishing.

Provenance, auditability, archival governance

ahgProvenancePlugin
Provenance capture and management separated from donor; provenance-linked reporting and export behaviour.

ahgAuditTrailPlugin
Audit trail capture for operational/compliance evidence; traceability of key actions.

ahgDonorAgreementPlugin
Donor agreement workflows/records and associated metadata.

Spectrum, loans, museum and sector workflows

ahgSpectrumPlugin
Spectrum-aligned procedures and workflows (movement/collection procedures, sector data, process tracking).

ahgLoanPlugin
Loan workflow management aligned to Spectrum (requests, approvals, movements, condition checks, tracking).

ahgMuseumPlugin
Museum-specific descriptive patterns and operational modules (objects/exhibitions/sector metadata).

ahgHeritageAccountingPlugin
Heritage asset accounting and valuation tracking support (reporting-aligned metadata and governance).

Preservation, condition, DAM, media, display

ahgPreservationPlugin
Preservation-oriented workflows and preservation metadata capture; operational preservation tooling.

ahgConditionPlugin
Condition assessment workflows (including photo evidence/annotation workflows where applicable).

ahgDAMPlugin
Digital Asset Management workflows: ingest coordination, asset handling patterns, derivative workflow integration.

ahgDisplayPlugin
Display/UX enhancements and presentation features across AtoM UI (viewer/UX improvements).

ahgGalleryPlugin
Gallery-style browsing/presentation features and curated display components.

ahgIiifCollectionPlugin
IIIF collection/manifest management workflows (collection-centric publishing patterns).

ahg3DModelPlugin
3D model attachment and display integration patterns (viewer support and associated metadata).

AI, extraction, search, research

ahgNerPlugin
Entity extraction workflow integration (people/places/organisations/dates) to enrich metadata and support redaction/lookup.

ahgMetadataExtractionPlugin
File/object metadata extraction and enrichment into AtoM fields (cross-plugin utility capability).

ahgSemanticSearchPlugin
Semantic search / embeddings-driven discovery patterns (where deployed and enabled).

ahgResearchPlugin
Researcher-oriented workflows and features (research UX and workflow enhancements).

ahgRicExplorerPlugin
RIC exploration and relationship navigation utilities (contextual exploration patterns).

ahgReportBuilderPlugin
Report builder framework: report definition, scheduling/export patterns, dashboard/report presentation utilities.

User engagement / productivity

ahgFavoritesPlugin
User favourites/bookmarks and personal organisation features.

ahgFeedbackPlugin
Feedback capture/moderation workflows (user interaction and quality improvement loop).

ahgCartPlugin
Cart/selection workflow for researchers/requests; optional integration point for e-commerce-like flows.

Integration, migration, operations

ahgAPIPlugin
Integration-oriented API surfaces/utilities (where applicable to your platform integration model).

ahgLibraryPlugin
Library-oriented collection patterns (catalogue-like workflows where required).

ahgMigrationPlugin
Migration scaffolding/utilities; controlled evolution patterns.

ahgDataMigrationPlugin
Data migration workflows and transformation orchestration.

ahgBackupPlugin
Operational backup tooling and related admin workflows.

ahgVendorPlugin
Vendor/party management utilities and shared dependency patterns.

Contribution model (critical)
What vendors should contribute

Vendors should build plugins and submit them via the catalog process.

Vendors should not modify the framework base unless explicitly requested and governed.

Naming conventions (enforced)

Reserved prefix: ahg is reserved for AHG-maintained plugins.

Third parties must use a unique vendor prefix: <vendorPrefix><Feature>Plugin.

machine_name == folder name == PluginConfiguration class prefix.

extension.json is required and authoritative for:

machine_name

version

requires (min framework/AtoM/PHP)

dependencies

category

Security

For security issues: prefer GitHub Security Advisories (where enabled).

For operational issues: open an issue in the relevant repository with environment details and reproduction steps.

Support

This ecosystem is designed for controlled deployments and repeatable upgrades:

Use the catalog/manifest to manage plugin versions.

Keep the framework stable; implement functionality in plugins.

Use shared SDKs to avoid duplicated client logic in UI modules and automation tooling.
