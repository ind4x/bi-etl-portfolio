# Business Intelligence & ETL Laboratory Portfolio

This repository hosts practical implementations, star schema data warehouse designs,
and Kettle ETL orchestration pipelines developed for the Business Intelligence (BI)
and Data Engineering curriculum at Mundiapolis University.

---

## Laboratory Overview

| Module | Category | Core Methodology | Primary Deliverables | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **[hotel-data-warehouse](./labs/lab4/hotel-data-warehouse)** | Academic Lab | Star schema modeling, Pentaho PDI dimension-first loading, master `.kjb` job orchestration | Data warehouse & KPI dashboard | [Lab](./labs/lab4/hotel-data-warehouse/README.md) |
| **[e-commerce-bi-assignment](./projects/e-commerce-bi-assignment)** | Major Project | E-Commerce logistics & sales analytics, carrier delivery delay metrics, Metabase visualization | PostgreSQL DW & Metabase charts | [Project](./projects/e-commerce-bi-assignment/README.md) |
| **[medical-center-bi](./projects/medical-center-bi)** | Major Project | Healthcare consultation tracking, physician workload analytics, financial revenue metrics | Star schema DW & Power BI reports | [Project](./projects/medical-center-bi/README.md) |

---

## General Running Instructions

### Prerequisites

- **Java Runtime:** OpenJDK 11 or 17 (required for Pentaho Data Integration / Kettle)
- **Database:** PostgreSQL 14+ (Local instance or Docker container)
- **ETL Tool:** Pentaho Data Integration (Spoon / Kitchen)
- **Visualization:** Metabase or Power BI Desktop

### Setup and Environment

1. **Clone the repository:**
   ```bash
   git clone git@github.com:ind4x/bi-etl-portfolio.git
   cd bi-etl-portfolio
   ```

2. **Database Provisioning (PostgreSQL):**
   Execute the target DDL table creation scripts located in each module's `sql/` or `scripts/sql/` directory:
   ```bash
   psql -U postgres -d postgres -f projects/e-commerce-bi-assignment/sql/table-creation-postgres.txt
   ```

3. **Executing ETL Jobs with Pentaho Kettle:**
   * **Via GUI (Spoon):** Launch `spoon.sh` and open the desired `.kjb` job or `.ktr` transformation.
   * **Headless execution (Kitchen):**
     ```bash
     kitchen.sh -file="projects/e-commerce-bi-assignment/etl/Job.kjb" -level=Basic
     ```

---

## Technology Stack

- **ETL Engine:** Pentaho Data Integration (PDI / Kettle Spoon 11)
- **Relational Databases:** PostgreSQL
- **Modeling Paradigms:** Dimensional Star Schema, Snowflaking, Kimball Methodology
- **BI Visualization:** Metabase, Power BI Desktop

---

## Author

- **Author:** Youssef Fellah ([ind4x_](https://github.com/ind4x))
- **Institution:** Mundiapolis University, Engineering Cycle
