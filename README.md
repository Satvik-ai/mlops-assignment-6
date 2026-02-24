# 🌸 Iris Classification ML Model — CI/CD Pipeline with FastAPI & Kubernetes

This project demonstrates a **production-ready machine learning deployment pipeline** that automates:

- Model training and validation  
- Continuous Integration (CI)  
- Containerization with Docker  
- Continuous Deployment (CD) to Kubernetes  

The pipeline builds an **Iris classification API** using **FastAPI**, packages it into a Docker image, pushes it to **Google Artifact Registry**, and deploys it to **Google Kubernetes Engine (GKE)** using **GitHub Actions**.

---

## 🎯 Assignment Objective

- Implement Continuous Deployment using GitHub Actions  
- Build Docker image for Iris API  
- Push image to Google Artifact Registry  
- Deploy containerized application on GKE  
- Maintain reproducible ML workflow using DVC and MLflow  

---

## 🧰 Tools & Technologies

- **Git** — Code versioning  
- **DVC** — Data versioning  
- **MLflow** — Experiment tracking & model registry  
- **GitHub Actions** — CI/CD automation  
- **FastAPI** — Model serving API  
- **Docker** — Containerization  
- **Google Artifact Registry** — Image storage  
- **Google Kubernetes Engine (GKE)** — Deployment  
- **Pytest & CML** — Testing and reporting  

---

## 🗂️ Repository Structure

```
├── data/ # Dataset tracked with DVC
│ └── iris.csv
├── artifacts/ # Trained model artifacts
├── src/
│ └── train.py # Training script with MLflow logging
├── tests/
│ ├── test_data_validation.py
│ └── test_model_evaluation.py
├── app/
│ ├── main.py # FastAPI app with /predict endpoint
│ ├── Dockerfile # Container build file
│ ├── requirements.txt # API dependencies
│ └── k8s/
│ └── deployment.yaml # Kubernetes deployment config
├── .github/workflows/
│ ├── ci-dev.yml # CI for dev branch
│ ├── ci-main.yml # CI for main branch
│ └── cd.yml # Continuous deployment pipeline
├── requirements.txt # Training dependencies
├── week6_GA_setup.ipynb # Setup notebook
└── README.md
```

---

## 📁 File Details

### 🔹 data/
Contains `iris.csv` dataset tracked using DVC.

---

### 🔹 artifacts/
Stores trained model files produced by training pipeline.

---

### 🔹 src/train.py

- Loads dataset  
- Trains a **Decision Tree classifier**  
- Logs parameters, metrics, and model to **MLflow**

---

### 🔹 tests/

#### test_data_validation.py
Validates dataset quality and schema.

#### test_model_evaluation.py
Ensures model meets performance threshold.

---

### 🔹 GitHub Actions Workflows

#### ci-dev.yml
Runs CI on **dev branch** pushes and PRs.

#### ci-main.yml
Runs CI on **main branch** pushes and PRs.

#### cd.yml
Triggers after successful CI on main branch:

1. Builds Docker image  
2. Pushes image to Artifact Registry  
3. Deploys to GKE  

---

### 🔹 app/

#### main.py
- Loads trained model  
- Creates FastAPI application  
- Exposes `/predict/` POST endpoint  

#### Dockerfile
- Builds lightweight Python container  
- Installs dependencies  
- Runs FastAPI using Uvicorn on port 8000  

#### k8s/deployment.yaml
- Deploys **2 replicas**  
- Exposes service via **LoadBalancer**  
- Maps port **80 → 8000**

---

### 🔹 week6_GA_setup.ipynb

Notebook used to:

- Initialize repository  
- Configure DVC remote  
- Create GitHub workflows  
- Push project to GitHub  

---

## 🔄 CI/CD Workflow Overview

1️⃣ Developer pushes code  
2️⃣ CI pipeline runs tests and validation  
3️⃣ On successful CI → CD pipeline triggers  
4️⃣ Docker image built and pushed to registry  
5️⃣ Kubernetes deploys updated API  
6️⃣ API becomes accessible via LoadBalancer  

---

## 🎥 Video Presentation  
[▶️ Click Here](https://drive.google.com/file/d/1B_gxLGtnjpzmZyiAjcSDmVxxZS8zm0Tj/view?usp=drive_link)
