# MLOps for Fraud Detection
**A Full-Stack Fraud Detection Pipeline (NUS DSA4288 Honours Year Project)**

[![Docker Image CI](https://github.com/ChinSekYi/mlops-fyp/actions/workflows/ci.yml/badge.svg)](https://github.com/ChinSekYi/mlops-fyp/actions/workflows/ci.yml)
[![CD - Staging](https://github.com/ChinSekYi/mlops-fyp/actions/workflows/cd-staging.yml/badge.svg)](https://github.com/ChinSekYi/mlops-fyp/actions/workflows/cd-staging.yml)
[![CD - Production](https://github.com/ChinSekYi/mlops-fyp/actions/workflows/ci-prod.yml/badge.svg)](https://github.com/ChinSekYi/mlops-fyp/actions/workflows/ci-prod.yml)

> **⚠️ Note:** This is a public copy of the project. The CI/CD badges above link to the original private repository where the automated pipelines are fully configured and operational. To set up CI/CD for this repository, refer to the documentation in `/docs/Developer_Guide/github-actions-secrets.md`.

## Overview
This project bridges the gap between academic research and industry-ready MLOps. Developed as a National University of Singapore (NUS) Honours Year Project under the supervision of **Prof. Markus Kirchberg**.

*   **The Problem:** Traditional notebook-based workflows lack the reproducibility and automation needed for production, leading to "models that perform well in development but fail in real-world applications".
*   **The Solution:** A multi-environment architecture (Dev, Staging, Prod) that reduced experiment setup time by **95%** (from 5 hours to <5 minutes) and eliminated manual logging errors.

---
## Use Case: Fraud Detection
This project demonstrates MLOps for traditional machine learning using a real-world fraud detection scenario. The goal is to identify fraudulent transactions from the PaySim synthetic financial dataset, helping financial institutions reduce losses and improve security.
<p align="center">
  <img src="https://github.com/user-attachments/assets/b2246763-574c-4819-8b32-8b25d989882e" width="700"/>
</p>

- Dataset: [Kaggle: Synthetic Financial Datasets For Fraud Detection (PaySim)](https://www.kaggle.com/datasets/ealaxi/paysim1)
- The dataset simulates mobile money transactions, including both normal and fraudulent activity, with features such as transaction type, amount, and account balances.

---
<p align="center">
  <a href="./docs/FinalReport_ChinSekYi.pdf"><b>📄 View Project Report</b></a> &nbsp;&nbsp; | &nbsp;&nbsp; <a href="./docs/Final_Presentation.pdf"><b>📊 View Presentation Slides</b></a>
</p>

---
## Technical Stack

| Category | Tools & Technologies |
| :--- | :--- |
| **Orchestration & CI/CD** | GitHub Actions (Automated Model Promotion) |
| **Tracking & Registry** | MLflow, PostgreSQL, AWS S3 |
| **Data Versioning** | DVC (Data Version Control) |
| **Serving & Frontend** | FastAPI (Inference), Streamlit (UI), Docker |
| **Infrastructure** | AWS EC2 (Isolated Multi-Environment Design) |

---
## Demo videos
| Demo 1: Data Scientist’s Development workflow | Demo 2: Model Promotion Workflow across Dev > Staging > Prod|
| :---: | :---: |
| <video src="https://github.com/user-attachments/assets/fe8c50fe-f72e-4e9b-8175-0fcdb15ebf6a" width="100%"></video> | <video src="https://github.com/user-attachments/assets/36370f12-9d37-4e70-9e5c-b8707ffd7e3f" width="100%"></video> |

---

## Architecture & System Design

### 1. End-to-End MLOps Blueprint
A high-level overview of the full ML lifecycle.
<p align="center">
  <img src="https://github.com/user-attachments/assets/bfb3e445-73fa-4254-a67e-13ae9bb64204" width="900" alt="Full MLOps Pipeline Blueprint"/>
</p>

* Data & Training: Automated pipelines featuring DVC for version control and a dedicated Feature Store.
* Deployment & CI/CD: Containerized FastAPI and Streamlit stacks deployed via GitHub Actions across Dev/Staging/Prod environments.
* Monitoring: Drift detection and performance monitoring using Evidently AI. (Roadmap Item)

### 2. MLflow Tracking & FastAPI Backend
An integrated workflow where the MLflow Tracking Server acts as the central hub for model versioning and artifact storage (S3). The FastAPI Backend dynamically queries the "Champion Model" from the registry to serve real-time predictions to clients via a REST API.
<p align="center">
  <img src="https://github.com/user-attachments/assets/08c7532a-cad0-45ed-9ca5-197e7148e31f" width="900" alt="MLflow FastAPI Backend"/>
</p>

### 3. Infrastructure & Environment Promotion
Cloud setup for Development, Staging, and Production environments on EC2.
<p align="center">
  <img src="https://github.com/user-attachments/assets/34a6c5a3-a4f4-4841-81e1-15091cb37e60" width="900" alt="Workflow Screenshot"/>
</p>

---

## File Structure
<details>
<summary>📂 <b>View Project File Structure</b></summary>
<br>
    
```text
mlops-fyp/
├── README.md                # Project overview and instructions
├── Makefile                 # Automation commands for setup, build, run, test
├── requirements.txt         # Python dependencies
├── artifacts/               # Saved model artifacts, metrics, and preprocessor objects
│   ├── metrics/
│   ├── models/
│   ├── preprocessor/
├── backend/                 # FastAPI backend API code
│   ├── main.py
│   ├── utils.py
├── configs/                 # Configuration files (YAML)
├── data/                    # Raw and processed datasets
│   ├── processed/
│   ├── raw/
├── docs/                    # All documentation, guides, and images
│   ├── Developer_Guide/     # Setup, infra, and developer docs
│   ├── User_Guide/          # Experimentation and serving guides
│   ├── images/              
├── env/                     # Environment variable files for each stage
├── frontend/                # Streamlit frontend app code
│   ├── app.py
│   ├── requirements.txt
│   ├── utils.py
├── infra/                   # Docker and deployment configs
│   ├── compose-files/
│   ├── docker/
├── model-promotion/         # Scripts for model promotion between stages
├── notebooks/               # Jupyter notebooks for exploration and analysis
├── requirements/            # Additional requirements files (base, ci)
├── src/                     # Core pipeline, components, and utilities
│   ├── components/
│   ├── core/
│   ├── pipeline/
├── tests/                   # Unit, integration, and e2e tests
```
</details>

---

## Getting Started

To explore the project, follow the documentation in the order below. For a full index of all guides, see the [Documentation Index](./docs/README.md).

1. Setup & Infrastructure
    * **Environment Setup:** Configure your [backend/frontend machines](./docs/Developer_Guide/backend-frontend-machine-setup.md) and [data management](./docs/Developer_Guide/data-management.md).
    * **Core Services:** Set up [Docker](./docs/Developer_Guide/docker-setup.md), [MLflow Tracking](./docs/Developer_Guide/mlflow-tracking-server-setup.md), and [Secrets/SSH](./docs/Developer_Guide/github-actions-secrets.md).

2. Usage & Workflow
    * **Experimentation:** Follow the [Model Experimentation Guide](./docs/User_Guide/model-experimentation-guide.md) to run DVC-tracked pipelines.
    * **Serving:** Deploy the model and interact with the UI via the [Model Serving Guide](./docs/User_Guide/model-serving-guide.md).

Recommended Reading Order:
1. Developer Guide (setup, environment, Docker, MLflow, SSH, secrets)
2. User Guide (experimentation, serving)


