# Hotel Analytics Data Warehouse & ETL Pipeline

This laboratory implements a complete Business Intelligence pipeline for a multi-branch
hospitality enterprise, modeling hotel reservations, booking channels, client demographics,
and revenue performance into a Kimball star schema using Pentaho Data Integration.

---

## Lab Structure

```text
hotel-data-warehouse/
├── README.md                          # Technical specification and architecture overview
├── data-sources/                      # Operational raw CSV extractions
│   ├── clients.csv                    # Customer profiles and contact details
│   ├── hotels.csv                     # Branch metadata, locations, and capacities
│   ├── chambres.csv                   # Room inventory and pricing tiers
│   ├── canaux.csv                     # Booking channels (Direct, OTA, Agency)
│   ├── reservations.csv               # Transactional booking records
│   └── temps.csv                      # Pre-calculated calendar dimension
├── etl-pipeline/                      # Pentaho Kettle orchestration
│   ├── orchestrator_job/              # Master execution job
│   │   └── hotel-etl-orchestrator.kjb # Master job enforcing dimension-first sequencing
│   └── transformations/               # Individual Kettle data transformation steps
│       ├── dimensions/                # load-dim-time.ktr, load-dim-hotel.ktr, load-dim-client.ktr
│       └── facts/                     # load-fact-reservation.ktr
└── reports/                           # Analytical dashboards
    └── dashboard-kpis.txt             # KPI specifications and occupancy rate formulas
```

### File Responsibilities

- **`data-sources/`**: Operational extracts simulating legacy transactional databases.
- **`etl-pipeline/`**: Modular Pentaho Data Integration (PDI) transformations handling surrogate key generation, data cleaning, date parsing, and fact table aggregations.
- **`reports/`**: KPI definitions tracking Average Daily Rate (ADR), Revenue Per Available Room (RevPAR), and channel distribution.

---

## Dimensional Architecture (Star Schema)

```text
       +-----------------------+              +-----------------------+
       |       dim_hotel       |              |       dim_client      |
       | - id_hotel (PK)       |              | - id_client (PK)      |
       | - nom, ville, etoiles |              | - nom, prenom, pays   |
       +-----------------------+              +-----------------------+
                   \                              /
                    \                            /
              +----------------------------------------+
              |          fact_reservation              |
              | - id_reservation (PK)                  |
              | - id_hotel (FK)                        |
              | - id_client (FK)                       |
              | - id_canal (FK)                        |
              | - id_temps (FK)                        |
              | - montant_total, nb_nuits, statut      |
              +----------------------------------------+
                    /                            \
                   /                              \
       +-----------------------+              +-----------------------+
       |       dim_canal       |              |       dim_temps       |
       | - id_canal (PK)       |              | - id_temps (PK)       |
       | - type_canal, nom     |              | - date, mois, annee   |
       +-----------------------+              +-----------------------+
```

---

## Execution Instructions

1. Open Pentaho Data Integration (Spoon).
2. Open the master job:
   ```text
   etl-pipeline/orchestrator_job/hotel-etl-orchestrator.kjb
   ```
3. Run the job to sequentially populate all dimensions before loading the fact table.

---

## Technology Stack

- **ETL Engine:** Pentaho Data Integration (PDI Spoon)
- **Modeling:** Dimensional Star Schema (Kimball)
- **Formats:** CSV, SQL

---

## Author

- **Author:** Youssef Fellah ([ind4x_](https://github.com/ind4x))
- **Institution:** Mundiapolis University, Engineering Cycle
