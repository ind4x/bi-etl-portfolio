# Medical Center Healthcare BI Solution

This project implements an end-to-end clinical and administrative decision-support
system for a healthcare facility, analyzing patient consultations, physician workload,
service efficiency, and financial streams using Pentaho PDI and PostgreSQL.

---

## Project Structure

```text
medical-center-bi/
├── README.md                          # Technical specification and architecture overview
├── RESPONSE.md                        # Academic responses to project specification questions
├── data/                              # Clinical raw operational records
│   ├── patients.csv                   # Patient demographic records
│   ├── medecins.csv                   # Physician identities and specializations
│   ├── services.csv                   # Medical departments and service offerings
│   ├── consultations.csv              # Patient consultation events and diagnosis logs
│   └── paiements.csv                  # Financial settlement transactions
├── scripts/sql/                       # Data Warehouse DDL Scripts
│   └── CRÉATION DES TABLES.txt        # Table schemas for dimensions and facts
├── etl/                               # Pentaho Kettle Transformation Pipelines
│   ├── Transformation-dim_patient.ktr
│   ├── Transformation-dim_medecin.ktr
│   ├── Transformation-dim_service.ktr
│   ├── Transformation-dim_paiement.ktr
│   ├── Transformation-dim_temps.ktr
│   └── Transformation-fact_consultation.ktr
└── docs/                              # Project documentation and graphical deliverables
    ├── reports/                       # Formal examination reports (PDF)
    └── images/                        # Transformation execution diagrams and dashboard previews
```

### File Responsibilities

- **`scripts/sql/CRÉATION DES TABLES.txt`**: Defines star schema tables with strict referential constraints.
- **`etl/`**: Pentaho PDI data cleaning pipelines handling nulls, type conversions, and surrogate key lookups.
- **`docs/reports/`**: Formal thesis report detailing healthcare KPIs and consultation wait times.

---

## Star Schema Architecture

```text
       +-----------------------+              +-----------------------+
       |       dim_patient     |              |       dim_medecin     |
       | - id_patient (PK)     |              | - id_medecin (PK)     |
       | - nom, age, genre     |              | - nom, specialite     |
       +-----------------------+              +-----------------------+
                   \                              /
                    \                            /
              +----------------------------------------+
              |           fact_consultation            |
              | - id_consultation (PK)                 |
              | - id_patient (FK)                      |
              | - id_medecin (FK)                      |
              | - id_service (FK)                      |
              | - id_paiement (FK)                     |
              | - id_temps (FK)                        |
              | - cout, duree_consult, satisfaction    |
              +----------------------------------------+
                    /                            \
                   /                              \
       +-----------------------+              +-----------------------+
       |       dim_service     |              |       dim_paiement    |
       | - id_service (PK)     |              | - id_paiement (PK)    |
       | - departement, batiment|             | - mode, statut        |
       +-----------------------+              +-----------------------+
```

---

## Execution Instructions

1. **Initialize Relational Schema:**
   ```bash
   psql -U postgres -d clinic_dw -f "scripts/sql/CRÉATION DES TABLES.txt"
   ```
2. **Execute ETL Pipelines:**
   Open each transformation in `etl/` inside Pentaho Spoon in dependency sequence (`dim_*` transformations first, followed by `fact_consultation`).
3. **Connect Reporting Tool:**
   Configure Power BI Desktop or Metabase to query `clinic_dw`.

---

## Technology Stack

- **Database:** PostgreSQL
- **ETL:** Pentaho Data Integration (PDI Spoon)
- **Reporting:** Power BI Desktop
- **Operating Environment:** Fedora Linux

---

## Author

- **Author:** Youssef Fellah ([ind4x_](https://github.com/ind4x))
- **Institution:** Mundiapolis University, Engineering Cycle
