# Flask-AKS-CICD-Pipeline
CI/CD Pipeline - Flask App Deployment on Azure Kubernetes Service (AKS)
Overview
This repository contains the CI/CD pipeline implementation for the Flask App Deployment on Azure Kubernetes Service (AKS) project. The pipeline automates the build, push, and deployment process using GitHub Actions, eliminating manual steps and ensuring every push to main delivers a fresh deployment to AKS.

Original Project
This pipeline extends the original Flask AKS deployment project, which covers:

Infrastructure provisioning with Terraform
Docker containerization and ACR image management
Kubernetes deployment with rolling updates
Real-world troubleshooting of pod failures and image pull errors
View the original project here: Flask-App-Deployment-on-Azure-Kubernetes-Service-AKS-

Technologies Used
Python / Flask
Docker
Azure Container Registry (ACR)
Azure Kubernetes Service (AKS)
GitHub Actions
Azure CLI
Azure Resources
Resource	Name
Resource Group	flask-aks-rg
AKS Cluster	flask-aks-cluster
Container Registry	flaskaksacr2026
Repository Structure

```mermaid
graph TD
 A[flask-aks-cicd/] --> B[.github/]
 A --> C[screenshots/]

 B --> B1[workflows/]
 B1 --> B2[deploy.yml]

 C --> C1[github-actions-success.png]
 C --> C2[acr-docker-image.png]
 C --> C3[aks-workload-running.png]
 C --> C4[flask-app-live.png]
 C --> C5[flask-app-live_1.png]
 C --> C6[flask-app-live_2_browser.png]

 style A fill:#0078D4,color:#fff
```
How the Pipeline Works
Every push to the main branch triggers the GitHub Actions workflow automatically. The pipeline runs the following steps in sequence:

Checks out the repository
Logs into Azure using GitHub Secrets
Builds the Docker image
Pushes the image to Azure Container Registry
Updates the AKS deployment with the new image
GitHub Secrets Required
Secret	Description
AZURE_CREDENTIALS	Azure service principal credentials
ACR_NAME	Azure Container Registry name
AKS_CLUSTER_NAME	AKS cluster name
AKS_RESOURCE_GROUP	Azure resource group name


Pipeline Screenshots
GitHub Actions - Successful Pipeline Run

Azure Container Registry - Docker Image Stored

AKS Workload - Flask App Pods Running

Live Flask App - Azure Portal Services View

Live Flask App - kubectl Service Output

Live Flask App - Browser Confirmation

Skills Demonstrated
CI/CD pipeline design and automation with GitHub Actions
Azure service principal authentication and GitHub Secrets management
Docker image build and push automation
Kubernetes rolling deployment automation
End-to-end cloud-native delivery pipeline on AKS
Maurrin Carter | Cloud Engineer | Azure | Kubernetes | Docker | GitHub Actions
