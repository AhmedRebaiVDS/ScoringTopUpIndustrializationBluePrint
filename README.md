# ScoringTopUpIndustrializationBluePrint


├── .azuredevops/  
│   ├── ml-pipelines.yml              # CI/CD workflows  
│   └── templates/  
│       ├── terraform-apply.yml       # Reusable Terraform steps  
│       ├── synapse-job.yml           # Synapse Spark job templates  
│       ├── aml-training.yml          # AML AutoML/model training  
│       ├── aks-deploy.yml            # AKS model deployment  
│       ├── data-ingestion.yml        # Data ingestion scripts  
│       ├── keyvault-secrets.yml      # Key Vault secret management  
│       └── monitoring-alerts.yml     # Azure Monitor alerts setup
├── infra/  
│   ├── main.tf                       # Root module  
│   ├── variables.tf                  # Global variables  
│   ├── modules/  
│   │   ├── data_lake/                # ADLS Gen2 + Delta Lake  
│   │   │   ├── storage.tf            # ADLS Gen2 containers  
│   │   │   └── delta_tables.tf       # Delta tables schema enforcement  
│   │   ├── synapse/                  # Synapse workspace, Spark pools  
│   │   ├── ml/                       # AML workspace, AKS  
│   │   └── security/                 # Key Vault, RBAC  
│   └── environments/  
│       ├── dev/  
│       │   ├── backend.tfvars        # Dev Terraform backend  
│       │   ├── variables.tfvars      # Dev-specific config (e.g., adls_name = "dev-datalake")  
│       │   └── .vault-env           # Key Vault name (hidden)  
│       ├── pre-prod/  
│       └── prod/  
└── app/  
    ├── data_ingestion/               # Python/PySpark scripts  
    │   ├── ingest_dwh.py             # Load data from DWH to ADLS  
    │   ├── ingest_hubspot.py         # Fetch HubSpot data via API  
    │   └── requirements.txt          # Libraries (delta-spark, requests, etc.)  
    ├── feature_engineering/          # Synapse notebooks/SQL scripts  
    ├── training/  
    │   ├── train_automl.py           # AML AutoML job  
    │   └── register_model.py         # Register model in AML  
    ├── deployment/  
    │   ├── aks_deploy.py             # Deploy model to AKS  
    │   └── kubernetes/               # K8s manifests  
    └── monitoring/  
        ├── drift_detection.py        # AML dataset monitors  
        └── alerts.json               # Azure Monitor alert rules
