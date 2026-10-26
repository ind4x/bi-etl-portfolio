# E-Commerce Sales & Logistics BI Analysis

This project models and analyzes transaction lifecycles for an e-commerce platform,
integrating commercial revenue indicators and logistics transport performance
into a star schema data warehouse connected to Metabase.

---

## Project Structure

```text
e-commerce-bi-assignment/
├── README.md                          # Technical specification and architecture overview
├── e-commerce-dashboard-performance.pdf # High-resolution export of supervisory dashboards
├── data/                              # Source operational datasets
│   ├── clients.csv                    # Customer segmentation and geographic attributes
│   ├── commandes.csv                  # Order headers and timestamps
│   ├── produits.csv                   # Catalog pricing and category taxonomy
│   └── transporteurs.csv              # Delivery partner identities and SLA thresholds
├── sql/                               # Relational Schema Definitions
│   └── table-creation-postgres.txt    # DDL scripts creating dimension and fact tables
├── etl/                               # Pentaho Data Integration (PDI) artifacts
│   ├── Job.kjb                        # Master orchestration job
│   ├── TR_Load_dim_client.ktr         # Client dimension loader
│   ├── TR_Load_dim_produit.ktr        # Product dimension loader
│   ├── TR_Load_dim_transporteur.ktr   # Logistics carrier dimension loader
│   ├── TR_Load_dim_temps.ktr          # Temporal hierarchy generator
│   └── TR_Load_fact_commande.ktr      # Central transactional order fact loader
└── docs/                              # Comprehensive business reports and screenshots
    ├── report_final.md                # Analytical thesis on commercial and carrier performance
    └── img/                           # Dashboard views and transformation graphs
```

### File Responsibilities

- **`sql/table-creation-postgres.txt`**: Declares PostgreSQL schemas with appropriate foreign keys and indexing.
- **`etl/Job.kjb`**: Orchestrator executing dimensional transformations in dependency order before triggering `TR_Load_fact_commande.ktr`.
- **`docs/report_final.md`**: Business analysis assessing late delivery rates and basket value optimization.

---

## Star Schema Architecture

```text
       +-----------------------+              +-----------------------+
       |       dim_client      |              |      dim_produit      |
       | - id_client (PK)      |              | - id_produit (PK)     |
       | - nom, ville, segment |              | - categorie, prix_un  |
       +-----------------------+              +-----------------------+
                   \                              /
                    \                            /
              +----------------------------------------+
              |           fact_commande                |
              | - id_commande (PK)                     |
              | - id_client (FK)                       |
              | - id_produit (FK)                      |
              | - id_transporteur (FK)                 |
              | - id_temps (FK)                        |
              | - quantite, montant_net, retard_jours  |
              +----------------------------------------+
                    /                            \
                   /                              \
       +-----------------------+              +-----------------------+
       |    dim_transporteur   |              |       dim_temps       |
       | - id_transp (PK)      |              | - id_temps (PK)       |
       | - nom_transp, delai   |              | - date, mois, trimestre|
       +-----------------------+              +-----------------------+
```

---

## Execution Instructions

1. **Deploy Tables:**
   ```bash
   psql -U postgres -d ecommerce_dw -f sql/table-creation-postgres.txt
   ```
2. **Execute ETL:**
   Open `etl/Job.kjb` in Pentaho Spoon and click **Run**.
3. **Supervision:**
   Connect Metabase to `ecommerce_dw` to explore the analytical dashboards.

---

## Technology Stack

- **Database:** PostgreSQL
- **ETL:** Pentaho Data Integration (Spoon 11)
- **Analytics Visualization:** Metabase
- **Operating Environment:** Fedora Linux

---

## Author

- **Author:** Youssef Fellah ([ind4x_](https://github.com/ind4x))
- **Institution:** Mundiapolis University, Engineering Cycle
