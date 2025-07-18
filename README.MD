# Automated Azure VM Deployment with GitHub Actions

Deploy an Azure Virtual Machine (VM) automatically using **Bicep** and **GitHub Actions**. This guide follows modern Markdown style and technical writing principles for clarity and developer productivity.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Step 1: Create a Resource Group](#step-1-create-a-resource-group)
- [Step 2: Create a Service Principal](#step-2-create-a-service-principal)
- [Step 3: Add Azure Credentials to GitHub Secrets](#step-3-add-azure-credentials-to-github-secrets)
- [Step 4: Push Deployment Files](#step-4-push-deployment-files)
- [References](#references)

## Prerequisites

- Azure CLI installed
- GitHub repository you control
- Azure subscription

## Step 1: Create a Resource Group

Use the Azure CLI to create a new resource group.

`az group create --name myResourceGroup --location eastus`



## Step 2: Create a Service Principal

Generate credentials so GitHub Actions can authenticate with your Azure account.

`az ad sp create-for-rbac
--name my-github-action-sp
--role contributor
--scopes /subscriptions/6eee05e7-464d-452d-b059-ca853975e441
--sdk-auth`


> **Note**: This command outputs a JSON object. Copy the entire output—you will use it in the next step.

## Step 3: Add Azure Credentials to GitHub Secrets

1. In your GitHub repository, navigate to  
   `Settings` → `Secrets and variables` → `Actions`.
2. Create a new secret:
   - **Name:** `AZURE_CREDENTIALS`
   - **Value:** Paste the JSON output from the previous step.

## Step 4: Push Deployment Files

Ensure these files exist in your repository:

- `vm-deploy.bicep`: Your Bicep template for defining the VM.
- `.github/workflows/deploy-vm.yml`: The GitHub Actions workflow.

Commit and push these files to your main branch:

`git add .
git commit -m "Add VM deployment pipeline"
git push origin main
`
text

> **Result:** GitHub Actions will automatically run the workflow and deploy your VM to Azure.
