# Awesome-Secure-Cross-Cloud-Data-Sharing

# Top Secure Cross-Cloud Data Sharing Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Zero-Copy Sharing, Open Protocols & Self-Hosted Data Exchange*  
**Last updated: October 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Secure Cross-Cloud Data Sharing**. These tools enable organizations to share data assets—tables, files, models—across clouds and organizational boundaries without copying or moving the underlying data, preserving governance, reducing egress costs, and enabling real-time collaboration.

**Examples** include Snowflake Secure Data Sharing, Databricks Delta Sharing, Google Analytics Data Share, AWS Data Exchange, Azure Data Share, Dawex, Revelate, Harbr, Informatica Cloud Data Marketplace, and Opendatasoft (the category leaders).

**Open-source emphasis**: Secure Cross-Cloud Data Sharing is a domain where open-source tooling is **anchored by a single foundational protocol but fragmented at the platform layer**. **Delta Sharing** is the de facto open standard—a Linux Foundation project with an Apache 2.0 licensed protocol and reference server that enables zero-copy sharing across Delta Lake, Apache Iceberg, and Parquet tables . The **OpenSharing** protocol extends this to a cross-platform, AI-native standard covering tables, volumes, ML models, and agent skills . For marketplaces, **data.all** provides an AWS-native data marketplace framework , and **UDAM** offers an API-first backend for monetizing data services . For privacy-preserving joint analysis, **SCQL** translates SQL into secure multi-party computation primitives . The critical caveat: **Delta Sharing's reference server is explicitly "not a completed implementation of secure web server"**—you must put it behind a secure proxy for public exposure . No open-source project replicates the **managed marketplace and governance experience** of Snowflake's Secure Data Sharing or AWS Data Exchange—those integrate procurement, billing, and runtime coupling that open-source cannot match.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-products)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Snowflake Secure Data Sharing](https://www.snowflake.com/)**  
  Native zero-copy sharing within Snowflake; providers create shares with object-level grants, consumers mount shared databases and query in real-time without data movement. The benchmark for governed B2B data collaboration, with Secure Views as a governance layer for row/column-level control .

- **[Databricks Delta Sharing](https://www.databricks.com/)**  
  Managed Delta Sharing service; providers share Delta Lake tables across clouds and platforms via the open protocol, with Databricks handling the server infrastructure and governance controls. The commercial offering built on the open-source protocol .

- **[Google Analytics Data Share](https://analytics.google.com/)**  
  Google's data sharing capabilities for Analytics properties; enables sharing of aggregated analytics data with Google services and linked products.

- **[AWS Data Exchange](https://aws.amazon.com/data-exchange/)**  
  AWS-native data marketplace with 3,500+ paid commercial listings; data delivered as files to S3 or via API, with purchases running through AWS billing against committed cloud spend.

- **[Azure Data Share](https://azure.microsoft.com/en-us/products/data-share)**  
  Microsoft's managed data sharing service; enables snapshot-based and in-place sharing across Azure tenants with governance controls.

- **[Dawex](https://www.dawex.com/)**  
  Data exchange platform for B2B data monetization and collaboration; positioned for organizations wanting a neutral marketplace for buying and selling data.

- **[Revelate](https://www.revelate.com/)**  
  Data marketplace and exchange platform; focuses on data product monetization and consumption analytics for data providers.

- **[Harbr](https://harbr.com/)**  
  Data collaboration and exchange platform; enables secure data sharing between organizations with governance and monetization features.

- **[Informatica Cloud Data Marketplace](https://www.informatica.com/)**  
  Data marketplace within Informatica's Intelligent Data Management Cloud; provides data discovery, access, and governance for internal and external data sharing.

- **[Opendatasoft](https://www.opendatasoft.com/)**  
  Data portal and sharing platform; focused on open data publication and internal data sharing with APIs and visualization tools.

## Open-Source GitHub Projects

### Open Sharing Protocols (Zero-Copy)

- **[Delta Sharing](https://github.com/delta-io/delta-sharing)**  
  The **foundational open protocol for secure zero-copy data sharing** (Apache 2.0, Linux Foundation) . Enables sharing Delta Lake tables across organizations and platforms without copying; the recipient reads directly from the provider's storage via short-lived, scoped credentials. Features: **REST API protocol**, reference server implementation (for testing and small deployments), **Apache Spark Connector** (SQL, Python, Java, Scala, R), and a growing connector ecosystem including **Power BI, Node.js, Rust, R, and Airflow** . Supports S3, Azure Blob Storage, and Azure Data Lake Storage Gen2 . **Critical caveat**: the reference server is **"not a completed implementation of secure web server"**—put it behind a secure proxy before exposing to the public . **The standard for open zero-copy sharing**—the protocol Databricks' managed service is built on.

- **[OpenSharing](https://github.com/OpenSharing-IO/OpenSharing)**  
  An **AI-native evolution of Delta Sharing** (Apache 2.0, Linux Foundation AI & Data project) . Extends the zero-copy model beyond tables to cover **Volumes** (files of any format), **Model** (ML artifacts with provenance), and **AgentSkill** (reusable AI agent capabilities) . Uses a three-level hierarchy (Share → Schema → Asset) with a **credential vending model** (AWS STS, Azure SAS, GCP OAuth, R2 tokens) so recipients read directly from provider storage. **Works where data lives**—S3, ADLS, GCS, R2, and on-premises. **Best for organizations wanting a vendor-neutral, AI-era sharing protocol** that covers models and agent skills alongside tables—but it is newer than Delta Sharing and the ecosystem is still developing .

### Data Marketplaces (Self-Hosted)

- **[data.all](https://github.com/data-dot-all/dataall)**  
  Open-source **data marketplace framework for AWS** (Apache 2.0) . Enables organizations to build an internal data marketplace where teams can produce, consume, and share data within and across business units. Built on AWS services (S3, Glue, Lake Formation, Redshift) with a modern web interface. Features: data discovery, access management, and collaboration across diverse users (analysts, scientists, engineers). **Best for AWS-native organizations** wanting a self-hosted internal data marketplace—but it is **AWS-only** and not designed for cross-cloud sharing .

- **[UDAM (Unified Data Marketplace)](https://github.com/data-agent-marketplace/data-agent-marketplace)**  
  Open-source, **API-first data marketplace backend** (Node.js/PostgreSQL) . Provides the transactional plumbing for monetizing data services: **listings management, Stripe payments, AES-256 encrypted token delivery, concurrency-safe order processing** (PostgreSQL row locks prevent overselling), session-based auth, and Docker-ready deployment . **For sellers**: create listings with pricing and units, manage API keys, automated token issuance on purchase. **For buyers**: browse, instant purchase for small orders, Stripe checkout for larger orders, token management . **Best for data sellers** wanting a self-hosted marketplace backend with payments—but it is a backend only (bring your own frontend) and does not provide zero-copy sharing or governance .

### Privacy-Preserving Collaboration

- **[SCQL (Secure Collaborative Query Language)](https://github.com/secretflow/scql)**  
  Open-source system that translates **SQL statements into Secure Multi-Party Computation (SMC) primitives** (Apache 2.0) . Enables multiple distrusting parties to run joint analysis **without revealing their private data**—the computation happens on encrypted inputs, and each party only sees the agreed-upon output. Executes on a federation of database systems. **Best for organizations needing joint analytics without data exposure**—for example, industry alliances calculating benchmarks, or supply chain partners computing shared risk scores—but it is **not a sharing protocol** (data is not exposed to recipients) and requires SMC infrastructure and expertise .

- **[secureflow](https://github.com/turtacn/secureflow)**  
  Open-source **secure multi-party data intelligence and collaboration platform** . Leverages **Federated Learning** (keeps raw data localized, exchanges only model parameters), **Multi-Party Computation** (encrypted aggregation, homomorphic encryption), **Confidential Computing** (TEEs like Intel SGX/AMD SEV), and **Blockchain** for audit trails and automated revenue sharing . Features: trusted data collaboration spaces, visual low-code data processing, pre-built industry model templates (supply chain risk, joint marketing), and smart contracts for revenue distribution . **Best for complex multi-party AI collaborations** requiring privacy-preserving joint model training—but it is **early-stage** and the build/run guide is still being updated .

### Additional Strong Open-Source Options

- **FQora** — Academic prototype for a **fair and quality-based data marketplace** (ACM Web Conference 2025) . Introduces quality-constrained queries, quality-based pricing functions, and Balanced Pareto Optimization to maximize utilities for both buyers and sellers. **Not production-ready**—a demonstration system for research on marketplace fairness and pricing .
- **Catalyst (orbisoperations)** — Federated data grid using **GraphQL stitching, Cloudflare Workers, and Zanzibar-inspired RelBAC** for real-time data sharing security . Designed for internet-scale, cloud-agnostic sharing without losing custody. **Niche**—verify maintenance status and production maturity, but the architecture (zero trust, asymmetric JWTs, edge deployment) addresses real cross-cloud sharing challenges .
- **Snowflake Data Sharing Tutorial (ElliottFairhall)** — Educational guide for mastering Snowflake Secure Data Sharing, including provider workflows, secure views, consumer mounting, and marketplace listings . **Not a platform**—a learning resource for teams implementing Snowflake sharing .

**Frameworks for building custom systems**: For **zero-copy table sharing across platforms**, Delta Sharing is the open standard with the broadest connector ecosystem . For **AI-era sharing including models and agent skills**, OpenSharing extends the model . For **AWS-native internal data marketplace**, data.all . For **monetizing data services with payments**, UDAM provides the transactional backend . For **joint analysis without data exposure**, SCQL or secureflow . No open-source project replicates the **managed marketplace, billing integration, and runtime coupling** of Snowflake Secure Data Sharing or AWS Data Exchange—those are commercial advantages.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Secure cross-cloud data sharing platforms handling sensitive data must comply with data licensing terms, privacy regulations (GDPR, CCPA), and organizational governance policies; **sharing data across organizational boundaries requires careful access control and audit trails**.
- **Open-source cross-cloud sharing is anchored by Delta Sharing but requires assembly for production**—Delta Sharing provides the protocol and reference server, but the reference server is **"not a completed implementation of secure web server"** and must be behind a secure proxy . OpenSharing extends the model to AI assets but is newer . No open-source project matches the **managed governance, billing integration, and marketplace experience** of Snowflake Secure Data Sharing or AWS Data Exchange—organizations requiring those capabilities should evaluate commercial platforms.
- Verify license terms for commercial use; Delta Sharing uses Apache 2.0 , OpenSharing uses Apache 2.0 , data.all uses Apache 2.0 , and UDAM is open-source (check repository) .

---

**Made for data platform engineers, governance architects, and organizations building cross-cloud data collaboration infrastructure.**  
Let's make secure cross-cloud data sharing more open, but with clear eyes about the secure proxy requirement and the managed marketplace gaps that commercial platforms still fill.
