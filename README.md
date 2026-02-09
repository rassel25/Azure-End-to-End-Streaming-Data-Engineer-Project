# 🎧 Azure Streaming Data Engineering Project

### *End-to-End Modern Data Platform with Streaming, Medallion Architecture, Unity Catalog & CI/CD*

[![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/)
[![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=flat&logo=databricks&logoColor=white)](https://databricks.com/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)](https://www.python.org/)
[![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C?style=flat&logo=apachespark&logoColor=white)](https://spark.apache.org/)

---

## 📌 Project Overview

This is an **end-to-end Azure Data Engineering portfolio project** designed to simulate real-world enterprise data platform implementation. The solution demonstrates how to build a scalable, production-grade data pipeline using modern Azure services and industry best practices.

The platform ingests data from **MS SQL Server**, processes it through a **Medallion Architecture (Bronze, Silver, Gold)**, and delivers analytics-ready datasets for business intelligence consumption.

### What Makes This Project Stand Out?

- **Production-Ready Design**: Follows enterprise standards with modular, reusable components
- **Advanced Techniques**: Implements SCD Type 2, streaming ingestion, and incremental loading
- **Modern Tech Stack**: Leverages cutting-edge Azure services and frameworks
- **DevOps Integration**: Full CI/CD implementation using GitHub and Databricks Asset Bundles
- **Enterprise Governance**: Unity Catalog for security, lineage, and access control

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| **Cloud Platform** | Microsoft Azure |
| **Languages** | Python (PySpark), SQL |
| **Source Database** | MS SQL Server |
| **Data Ingestion** | Azure Data Factory (ADF) |
| **Data Processing** | Azure Databricks (PySpark) |
| **Storage** | Azure Data Lake Storage Gen2 (ADLS Gen2) |
| **Streaming** | Spark Structured Streaming & Auto Loader |
| **Automation** | Logic Apps |
| **Data Modeling** | Star Schema, SCD Type 2 |
| **Orchestration** | Delta Live Tables (DLT) & ADF |
| **Governance** | Unity Catalog |
| **Version Control** | GitHub |
| **CI/CD** | Databricks Asset Bundles |

---

## 🏗️ Architecture Overview

<img width="1301" height="784" alt="Screenshot 2026-02-09 172909" src="https://github.com/user-attachments/assets/4b928f4e-3d7a-43c1-ae59-8cc2f8aee138" />

```
┌─────────────────┐
│   MS SQL Server │ (Source)
│  Spotify Dataset│
└────────┬────────┘
         │
         │ Azure Data Factory (ADF)
         │ - Incremental Loading
         │ - Backfill Support
         │ - Dynamic Pipelines
         ▼
┌─────────────────────────────────────────────────────────┐
│                  Azure Data Lake Gen2                   │
│ ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│ │    BRONZE    │  │    SILVER    │  │     GOLD     │  │
│ │  Raw Parquet │→ │ Cleaned Data │→ │ Star Schema  │  │
│ │              │  │ Auto Loader  │  │  SCD Type 2  │  │
│ └──────────────┘  └──────────────┘  └──────────────┘  │
└─────────────────────────────────────────────────────────┘
         ▲                 ▲                 ▲
         │                 │                 │
    Azure Data       Azure Databricks   Delta Live Tables
     Factory         Spark Streaming         (DLT)

```

### Data Flow Explanation

**Source Layer**
- **MS SQL Server** hosting a simulated Spotify dataset

**Bronze Layer (Raw Data)**
- Raw data ingestion via **Azure Data Factory (ADF)**
- Stored in **Parquet format** in Azure Data Lake Storage Gen2
- Parameterized, reusable pipelines with Git integration
- Support for both incremental and backfill loading patterns

**Silver Layer (Processed Data)**
- Data transformation using **Azure Databricks** with PySpark
- **Spark Structured Streaming & Auto Loader** for near real-time processing
- Data cleaning, validation, deduplication, and enrichment
- Schema evolution handling and data quality checks

**Gold Layer (Curated Data)**
- **Star Schema** implementation (Fact & Dimension tables)
- **Slowly Changing Dimensions (SCD Type 2)** for historical tracking
- Built with **Delta Live Tables (DLT)** for declarative ETL
- Analytics-ready datasets optimized for BI consumption

**DevOps & Governance**
- **Unity Catalog** for centralized access control, data lineage, and metadata management
- Fine-grained permissions and secure data sharing
- **CI/CD Integration** with GitHub workflows

---

## 🚀 Key Features

### Data Ingestion
- ✅ **Incremental Loading** with JSON Metadata approach for efficient data extraction
- ✅ **Backfill Capability** for historical data reprocessing
- ✅ **Dynamic Pipelines** in ADF with parameterization for reusability
- ✅ **Self-hosted Integration Runtime** support for hybrid cloud scenarios

### Data Processing
- ✅ **Streaming Ingestion** using Spark Structured Streaming
- ✅ **Auto Loader** for efficient file ingestion with schema evolution
- ✅ **Data Quality Checks** and validation rules
- ✅ **Error Handling** and dead letter queue implementation

### Data Modeling
- ✅ **Star Schema Design** with fact and dimension tables
- ✅ **SCD Type 2 Implementation** using Delta Live Tables for complete historical tracking
- ✅ **Surrogate Keys** and natural key management
- ✅ **Referential Integrity** enforcement

### DevOps & Governance
- ✅ **CI/CD Integration** with GitHub workflows
- ✅ **Databricks Asset Bundles** for automated deployment
- ✅ **Unity Catalog** for enterprise-grade governance
- ✅ **Data Lineage** tracking and impact analysis
- ✅ **Modular Design** for maintainability and scalability

---

## 📂 Project Structure

```
spotify-azure-data-engineering/
│
├── README.md
├── LICENSE
│
├── source_dataset/
│   ├── initial_dataset.sql             # DDL for source database and initial data generation
│   └── incremental_dataset.sql         # incremental data generation
│
├── pipeline/
│   ├── pipelines/
│   │   ├── incremental_ingestion.json # Incremental load pipeline
│   │   ├── backfill_pipeline.json     # Historical backfill pipeline
│   │   └── orchestrator.json          # Master pipeline
│   ├── datasets/
│   │   ├── sql_source_dataset.json    # SQL Server connection
│   │   └── adls_sink_dataset.json     # Data Lake connection
│   └── linked_services/
│       ├── sql_server_ls.json         # SQL Server linked service
│       ├── adls_gen2_ls.json          # ADLS Gen2 linked service
│       └── databricks_ls.json         # Databricks linked service
│
├── databricks_notebooks/
│   ├── bronze/
│   │   └── raw_data_landing.py        # Bronze layer ingestion logic
│   ├── silver/
│   │   ├── stream_artists.py          # Artist dimension streaming
│   │   ├── stream_tracks.py           # Track dimension streaming
│   │   ├── stream_users.py            # User dimension streaming
│   │   └── stream_plays.py            # Plays fact streaming
│   ├── gold/
│   │   ├── dlt_star_schema.py         # DLT pipeline definition
│   │   ├── dim_artists_scd2.py        # SCD Type 2 for artists
│   │   ├── dim_users_scd2.py          # SCD Type 2 for users
│   │   └── fact_plays.py              # Fact table creation
│   └── utilities/
│       ├── config.py                  # Configuration management
│       ├── helpers.py                 # Reusable helper functions
│       └── data_quality.py            # Quality check functions
│
├── asset_bundles/
│   ├── databricks.yml                 # Asset bundle configuration
│   └── resources/
│       ├── jobs.yml                   # Job definitions
│       └── pipelines.yml              # DLT pipeline definitions
│
├── ci_cd/
│   └── .github/
│       └── workflows/
│           ├── deploy_dev.yml         # Dev environment deployment
│           └── deploy_prod.yml        # Prod environment deployment
│
└── docs/
    ├── architecture.md                # Detailed architecture docs
    ├── setup_guide.md                 # Step-by-step setup
    └── scd2_implementation.md         # SCD Type 2 explanation
```

---

## 🔄 Data Pipeline Flow

### End-to-End Process

1. **Extract** → ADF extracts data from MS SQL Server using incremental or backfill patterns
2. **Land** → Raw data lands in Bronze layer (ADLS Gen2) in Parquet format
3. **Stream** → Databricks Auto Loader detects new files and triggers Spark Structured Streaming
4. **Transform** → Silver layer notebooks clean, validate, and enrich the data
5. **Model** → Delta Live Tables build Star Schema with SCD Type 2 in Gold layer
6. **Serve** → Curated data exposed via Databricks SQL Warehouse for analytics

### Azure Data Factory Pipeline

<img width="1034" height="282" alt="adf" src="https://github.com/user-attachments/assets/9a65b541-9786-41ab-ae0b-d6168f21ad46" />

<img width="1088" height="364" alt="adf2" src="https://github.com/user-attachments/assets/5a1a02a7-0d7b-4321-a83a-221e081bdf85" />

<img width="920" height="237" alt="adf3" src="https://github.com/user-attachments/assets/0e787a72-de30-4334-b811-1e6320e89cf0" />

<img width="885" height="193" alt="adf4" src="https://github.com/user-attachments/assets/3ca4553b-b8de-43e6-aae2-e8ccef894c14" />


---

## 🚀 Getting Started

### Prerequisites

- Azure Subscription with appropriate permissions
- GitHub account for version control
- Basic knowledge of SQL, Python, and Spark
- Understanding of data engineering concepts

### Step-by-Step Setup

#### 1. Provision Azure Resources

```bash
# Create Resource Group
az group create --name rg-spotify-data-platform --location eastus

# Create Storage Account (ADLS Gen2)
az storage account create \
  --name sadatalakespotify \
  --resource-group rg-spotify-data-platform \
  --location eastus \
  --sku Standard_LRS \
  --kind StorageV2 \
  --hierarchical-namespace true

# Create containers: bronze, silver, gold
az storage container create --name bronze --account-name sadatalakespotify
az storage container create --name silver --account-name sadatalakespotify
az storage container create --name gold --account-name sadatalakespotify
```

#### 2. Set Up Source Database

```sql
-- Run source_scripts/create_source_tables.sql
-- Run source_scripts/insert_sample_data.sql
```

#### 3. Configure Azure Data Factory

- Create ADF instance
- Set up Linked Services (SQL Server, ADLS Gen2, Databricks)
- Configure Self-hosted Integration Runtime (if needed)
- Import and configure pipeline JSON files
- Set up pipeline parameters and triggers

#### 4. Configure Azure Databricks

- Create Databricks workspace with Unity Catalog enabled
- Set up compute clusters
- Import notebooks from `databricks_notebooks/`
- Configure secrets for authentication
- Set up Unity Catalog metastore and catalogs

#### 5. Deploy Pipelines

```bash
# Initialize Databricks Asset Bundle
databricks bundle init

# Validate configuration
databricks bundle validate

# Deploy to development
databricks bundle deploy --target dev

# Deploy to production
databricks bundle deploy --target prod
```

#### 6. Run the Pipeline

- Trigger ADF pipelines for initial backfill
- Enable incremental loading schedule
- Monitor Databricks streaming jobs
- Execute DLT pipeline for Gold layer
- Validate data in SQL Warehouse

---

## 📊 Sample Dataset

The project uses a simulated **Spotify dataset** with the following tables:

### Source Tables (MS SQL Server)

| Table | Description | Key Columns |
|-------|-------------|-------------|
| **Artists** | Artist master data | artist_id, name, genre, country, popularity |
| **Users** | User profiles | user_id, username, email, country, subscription_type |
| **Tracks** | Song catalog | track_id, title, artist_id, album, duration_ms, release_date |
| **Plays** | User listening history | play_id, user_id, track_id, played_at, duration_played |

### Gold Layer (Star Schema)

**Fact Table**
- `fact_plays`: Granular play events with foreign keys to dimensions

**Dimension Tables (SCD Type 2)**
- `dim_artists`: Artist attributes with historical tracking
- `dim_users`: User profiles with subscription changes over time
- `dim_tracks`: Track metadata (Type 1 slowly changing)
- `dim_date`: Date dimension for time-based analysis

---

## 🎯 Learning Outcomes

By working through this project, you will master:

### Technical Skills
- Building production-grade Azure data pipelines
- Implementing Medallion Architecture (Bronze, Silver, Gold)
- Streaming data processing with Spark Structured Streaming
- Advanced data modeling (Star Schema & SCD Type 2)
- Delta Lake and Delta Live Tables
- Unity Catalog governance and security

### Engineering Practices
- Incremental and backfill data loading strategies
- CI/CD for data engineering workflows
- Modular and reusable code design
- Error handling and monitoring
- Data quality validation frameworks
- Documentation and knowledge sharing

### Cloud & DevOps
- Azure resource management and networking
- Infrastructure as Code principles
- Git-based version control for data assets
- Environment promotion (Dev → QA → Prod)
- Cost optimization techniques

---

## 📈 Future Enhancements

Potential improvements and extensions:

- [ ] Add real-time dashboards using Power BI or Tableau
- [ ] Implement data quality monitoring with Great Expectations
- [ ] Add machine learning models for recommendation systems
- [ ] Set up alerting and monitoring with Azure Monitor
- [ ] Implement data masking for PII protection
- [ ] Add integration tests and unit tests
- [ ] Create Terraform/Bicep templates for infrastructure deployment
- [ ] Implement row-level security in Unity Catalog
- [ ] Add cost tracking and optimization dashboard

---

## 🤝 Contributing

Contributions are welcome! If you have suggestions for improvements:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -m 'Add some feature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 📚 Additional Resources

### Official Documentation
- [Azure Data Factory Documentation](https://docs.microsoft.com/azure/data-factory/)
- [Azure Databricks Documentation](https://docs.databricks.com/azure/)
- [Delta Lake Documentation](https://docs.delta.io/)
- [Unity Catalog Documentation](https://docs.databricks.com/data-governance/unity-catalog/)

### Related Learning
- [Medallion Architecture Best Practices](https://www.databricks.com/glossary/medallion-architecture)
- [SCD Type 2 Implementation Guide](https://www.databricks.com/blog/2019/08/09/scd-type-2-slowly-changing-dimensions.html)
- [Spark Structured Streaming Guide](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html)

---

## 🙌 Acknowledgements

This project is inspired by real-world enterprise Azure data engineering workflows and modern industry standards. Special thanks to the data engineering community for sharing knowledge and best practices.

---

## 📧 Contact

For questions, feedback, or collaboration opportunities:

- **GitHub Issues**: [Create an issue](../../issues)
- **LinkedIn**: [Your LinkedIn Profile]
- **Email**: your.email@example.com

---

<div align="center">

⭐ **If you find this project useful, please consider giving it a star!** ⭐

**Happy Data Engineering!** 🚀

</div>
