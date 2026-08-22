Got it. The README already has a Pipeline Screenshots section with all six images. The image syntax needs fixing though - they're showing as plain text links instead of rendered images. Here is the full corrected README:

CI/CD Pipeline - Flask App Deployment on Azure Kubernetes Service (AKS)

Overview

This repository contains the CI/CD pipeline implementation for the Flask App Deployment on Azure Kubernetes Service (AKS) project. The pipeline automates the build, push, and deployment process using GitHub Actions, eliminating manual steps and ensuring every push to main delivers a fresh deployment to AKS.

Original Project

This pipeline extends the original Flask AKS deployment project, which covers:
- Infrastructure provisioning with Terraform
- Docker containerization and ACR image management
- Kubernetes deployment with rolling updates
- Real-world troubleshooting of pod failures and image pull errors

View the original project here: Flask-App-Deployment-on-Azure-Kubernetes-Service-AKS (https://github.com/maxmagnac/Flask-App-Deployment-on-Azure-Kubernetes-Service-AKS-)

Technologies Used

- Python / Flask
- Docker
- Azure Container Registry (ACR)
- Azure Kubernetes Service (AKS)
- GitHub Actions
- Azure CLI

Azure Resources

| Resource | Name |
|---|---|
| Resource Group | flask-aks-rg |
| AKS Cluster | flask-aks-cluster |
| Container Registry | flaskaksacr2026 |

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

1. Checks out the repository
2. Logs into Azure using GitHub Secrets
3. Builds the Docker image
4. Pushes the image to Azure Container Registry
5. Updates the AKS deployment with the new image

GitHub Secrets Required

| Secret | Description |
|---|---|
| AZURE_CREDENTIALS | Azure service principal credentials |
| ACR_NAME | Azure Container Registry name |
| AKS_CLUSTER_NAME | AKS cluster name |
| AKS_RESOURCE_GROUP | Azure resource group name |

Pipeline Screenshots

GitHub Actions - Successful Pipeline Run


GitHub Actions Success
<img width="997" height="439" alt="github-actions-success" src="https://github.com/user-attachments/assets/06b3d478-2447-4db4-8cd9-9d5bc854e01d" />



Azure Container Registry - Docker Image Stored
<img width="1457" height="531" alt="acr-docker-image" src="https://github.com/user-attachments/assets/2f61b7c9-1ef8-41e8-b445-03a0bd2f1d40" />


AKS Workload - Flask App Pods Running
<img width="1231" height="828" alt="aks-workload-running" src="https://github.com/user-attachments/assets/bbd06ffa-e9c6-4310-b026-47236488110f" />



Live Flask App - Azure Portal Services View
<img width="1592" height="473" alt="flask-app-live" src="https://github.com/user-attachments/assets/32cf71a0-53cd-4001-ae93-4253b896e09b" />



Live Flask App - kubectl Service Output
<img width="749" height="86" alt="flask-app-live_1" src="https://github.com/user-attachments/assets/0108cc95-c0bc-4f9b-a90d-1cec3c6aef87" />


Live Flask App - Browser Confirmation

<img width="456" height="178" alt="flask-app-live_2_browser" src="https://github.com/user-attachments/assets/86e7e21e-a94c-473a-a2cf-174c8c9cbddc" />




Lessons Learned

Azure Credentials Configuration
Configuring the AZURE_CREDENTIALS secret required generating a service principal with the correct role assignments. The JSON output from the az ad sp create-for-rbac command maps directly to the GitHub secret - formatting errors in that JSON block caused initial authentication failures. Validating the JSON structure before saving it as a secret resolved the issue.

YAML Syntax in GitHub Actions
GitHub Actions workflows are strict about indentation and spacing. A single misaligned step or missing colon caused the entire pipeline to fail at parse time. Reading the error output in the Actions tab carefully and validating the YAML with a linter before pushing saved significant troubleshooting time.

AKS Deployment Timing
After pushing a new image to ACR, the AKS deployment update requires a moment to pull and spin up the new pod. Building a clear understanding of rolling update behavior - and using kubectl get pods to monitor pod status - helped confirm successful deployments.

Skills Demonstrated

- CI/CD pipeline design and automation with GitHub Actions
- Azure service principal authentication and GitHub Secrets management
- Docker image build and push automation
- Kubernetes rolling deployment automation
- End-to-end cloud-native delivery pipeline on AKS

Maurrin Carter | Cloud Engineer | Azure | Kubernetes | Docker | GitHub Actions
