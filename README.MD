1. Create Resource Group
bash
az group create --name myResourceGroup --location eastus
2. Create Service Principal
bash
az ad sp create-for-rbac --name my-github-action-sp --role contributor --scopes /subscriptions/6eee05e7-464d-452d-b059-ca853975e441 --sdk-auth
Copy the JSON output.

3. Add to GitHub Secrets
Go to repository → Settings → Secrets and variables → Actions

Create secret named AZURE_CREDENTIALS

Paste the JSON from step 2

4. Push Files to Main Branch
vm-deploy.bicep (Bicep template)

.github/workflows/deploy-vm.yml (GitHub Actions workflow)

GitHub Actions automatically triggers and deploys your VM successfully.
