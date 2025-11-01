# Iris Classification ML Model - CI/CD Pipeline

**MLOps - Week 6 - Assignment - 21f1000344**

## Assignment Objective : 
- Develop and integrate Continuous Deployment using GitHub Actions for building the IRIS API using docker and deploying onto k8s (kubernetes)
- Use GitHub workflows/actions to build the docker image using DockerFile
- Push the image to Google Artifact Registry 
- Deploy it using Google Kubernetes Engine from GitHub Actions

## Tools Used :
- Git for code versioing
- DVC for data versioning
- MLFlow for model versioning, expermiment tracking and reproducibility
- GitHub Actions for Continuous Integration and Continuous Deployment
- FastAPI for serving the model via `/predict/` endpoint
- Docker for creating image
- Google Artifact Registry for storing the docker image
- Google Kubernetes Engine for running the instance of the docker image


---

## Files

### 1. `data` folder
- **Key Utilities:**
  - Stores `iris.csv` data

### 2. `artifacts` folder
- **Key Utilities:**
  - Stores the trained iris classification model

### 3. `src/train.py`
- **Key Utilities:**
  - Loads the `iris.csv` 
  - Trains a `Decision Tree` model
  - Logs experiment parameters, eval metrics and models utilizing MLFlow

### 4. `tests/test_data_validation.py` and `tests/test_model_evaluation`
- **Key Utilities:**
  - Runs unit tests using pytest on data and model

### 5. `requirements.txt`
- **Key Utilities:**
  - List of required packages for the Continuous Integration (CI) with GitHub Actions

### 6. `.github/worflows/ci-dev.yml` and `.github/worflows/ci-main.yml`
- **Key Utilities:**
  - YAML file for configuring GitHub Actions to perform Continuous Integration (CI)
  - `ci-dev.yml` perfroms CI for `dev` branch on push and pull request
  - `ci-main.yml` perfroms CI for `main` branch on push and pull request
  - On push, CI for the respective branch will be triggered
  - On pull request, CI for the both the branch be triggered
  - Fetches the model and data needed for evaluation from DVC
  - Runs sanity test and prints report as a comment using cml

### 7. `.github/worflows/cd.yml`
- **Key Utilities:**
  - YAML file for configuring GitHub Actions to perform Continuous Deploymement (CD)
  - Gets triggered after a successful CI on main branch
  - Builds the docker image using DockerFile
  - Pushes the image to Google Artifact Registry
  - Deploys the container image of Iris FastAPI application on Google Kubernetes Engine

### 8. `app` folder
- **Key Utilities:**
  - Serves as the root directory for deployment
  - `main.py` :- Loads the model, creates a FastAPI app, and builds a `/predict/` endpoint which accepts a post request with features in the body and serves the predicted classification label
  - `Dockerfile` :- It is used to create image that spuns out a lightweight Python 3.10 container to run a FastAPI application with its dependencies and model files using Uvicorn on port 8000
  - `k8s/deployment.yaml` :- Deploys two replicas of the Iris FastAPI application (using the specified container image) and exposes it externally via a LoadBalancer service that maps port 80 to container port 8000
  - `requirements.txt` :- Contains the list of packages needed for running the main.py. Dockerfile uses it to download the dependencies

### 9. `week6_GA_setup.ipynb`
- **Key Utilities:**
  - Created in Vertex AI workbench
  - Serves as an interface for performing actions local working directory
  - Setup Git Repository with `dev` and `main` branch
  - Setup DVC with GCS bucket as remote storage
  - Created YAML file for GitHub Actions
  - Pushed the local working directory to remote repo on GitHub

---
