<h1>Azure Storage Security and Network Isolation</h1>

<h2>Description</h2>
Deploys a secure Azure storage account with public access disabled, configures a private endpoint for network-isolated access, generates a SAS token for scoped access testing, and enforces a storage security policy through Azure Policy. Demonstrates storage hardening and network isolation concepts relevant to any cloud or sysadmin role.
<br>
<br>


<h2>Utilities Used</h2>

- <b>Azure CLI — storage account deployment and verification</b>
- <b>Azure Portal — private endpoint configuration and policy assignment</b>
- <b>Azure Storage Explorer — blob access testing</b>
- <b>Azure Policy — built-in policy assignment for compliance</b>
- <b>Azure Bicep — storage account as IaC (simple template)</b>

<h2>Environments Used </h2>

- <b>Windows 11 (local workstation)</b>
- <b>Azure Cloud Shell (deployment and CLI commands)</b>
- <b>Azure Portal (private endpoint, policy, verification)</b>
- <b>Azure Storage Explorer (blob upload/download testing)</b>

<h2>Lab Architecture</h2>

<h2>Program walk-through:</h2>

<p align="center">
<h align="center">
<h3>Step 1 — Deploy Storage Infrastructure with Bicep</h3>
<br />
Create storage.bicep, paste in the template below, then deploy it from Azure Cloud Shell. The template deploys a hardened storage account with public access disabled, HTTPS enforced, and a default network deny rule. <br/>
<br/>
<img src="https://github.com/user-attachments/assets/84125cee-3f0b-4dd4-a1db-7270b5d96e56" height="80%" width="80%" alt="Azure Resource Group"/>
<br />
<br />
<img src="https://github.com/user-attachments/assets/6369428a-0a13-4dd6-92b9-7a55428914f8" height="80%" width="80%" alt="Azure Resource Group"/>
<br />
<br />
<br />
<h3>Step 2 — Create a VNet and Private Endpoint via CLI</h3>
<br />
Deploy a virtual network with a private subnet, then create a private endpoint to allow network-isolated access to the storage account without any traffic touching the public internet. <br/>
<br/>
<img src="https://github.com/user-attachments/assets/730948b0-11a7-4801-b613-a37b54e83d47" height="80%" width="80%" alt="Bicep Deployment"/>
<br />
<br />
<img src="https://github.com/user-attachments/assets/d60e83b3-cc46-4665-a728-e6768b87eb53" height="80%" width="80%" alt="Bicep Deployment"/>
<br />
<br />
<img src="https://github.com/user-attachments/assets/525f959d-f23b-4258-a1b4-2ace68fc7fe1" height="80%" width="80%" alt="Bicep Deployment"/>
<br />
<br />
<img src="https://github.com/user-attachments/assets/b4e64a2c-a17b-4ad8-9bac-260c5b52eeb0" height="80%" width="80%" alt="Bicep Deployment"/>
<br />
<br />
<br />
<h3>Step 3 — Verify Security Configuration</h3>
<br />
Run the following commands to confirm public access is disabled, network rules are set to deny, and the private endpoint provisioned successfully. The failed curl response is expected and confirms the configuration is working correctly. <br/>
<br/>
<img src="https://github.com/user-attachments/assets/084bdf67-7907-48d0-b05c-2bd869e86003" height="80%" width="80%" alt="VM-NSG Confirmation"/>
<br />
<br />
<img src="https://github.com/user-attachments/assets/ef4e2ed7-33cf-410c-b1b1-b8198d60b947" height="80%" width="80%" alt="VNET Confirmation"/>
<br />
<br />
<img src="https://github.com/user-attachments/assets/6a55dc94-20c2-4cad-aabe-1017bff76908" height="80%" width="80%" alt="VNET Confirmation"/>
<br />
<br />
<br />
<h3>Step 4 — Create a Blob Container and Test with SAS Token</h3>
<br />
Create a blob container, generate a time-limited SAS token, then use Azure Storage Explorer to upload and download a test file to confirm scoped access works correctly. <br/>
<br/>
<img src="https://github.com/user-attachments/assets/f397724e-ab41-49f1-9ade-5fa2f32194b9" height="80%" width="80%" alt="Shared Drive"/>
<br />
<br />
<img src="https://github.com/user-attachments/assets/7da8d835-6c25-41dd-9e4d-6475339c3c31" height="80%" width="80%" alt="Shared Drive"/>
<br />
<br />
<img src="https://github.com/user-attachments/assets/3150efde-f8a8-482a-9322-397c78b797b9" height="80%" width="80%" alt="Shared Drive"/>
<br />
<br />
<img src="https://github.com/user-attachments/assets/c6d677c8-e5ec-4528-8414-a88eb1f66ba2" height="80%" width="80%" alt="Shared Drive"/>
<br />
<br />
<br />
<h3>Step 5 — Assign a Built-in Azure Policy</h3>
<br />
Navigate to Azure Policy > Definitions, search for "Secure transfer to storage accounts should be enabled", click Assign, set the scope to rg-lab03, and click Review and Create. Wait 15-20 minutes then navigate to rg-lab03 > Policies to review the compliance state.  <br/>
<br/>
<img src="https://github.com/user-attachments/assets/4a41e155-6bcf-404e-855b-355796ccd780" height="80%" width="80%" alt="Password Policy GPO Linked to Domain"/>
<br />
<br />
<h3>Step 6 — Cleanup</h3>
<br />
Delete the resource group to remove all provisioned resources and avoid ongoing charges.  <br/>
<br/>
<img src="https://github.com/user-attachments/assets/ca08c0f8-4de5-443e-9357-b8fc98f27248" height="80%" width="80%" alt="Password Policy GPO Linked to Domain"/>
<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
