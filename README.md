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
<img src="https://github.com/user-attachments/assets/a70c0f74-b170-46e2-b401-eac67c98a683" height="80%" width="80%" alt="Azure Resource Group"/>
<br />
<br />
<br />
<h3>Step 2 — Create a VNet and Private Endpoint via CLI</h3>
<br />
Deploy a virtual network with a private subnet, then create a private endpoint to allow network-isolated access to the storage account without any traffic touching the public internet. <br/>
<br/>
<img src="https://github.com/user-attachments/assets/d7fc65fa-322c-4440-804f-b3481ef546b7" height="80%" width="80%" alt="Bicep Deployment"/>
<br />
<br />
<br />
<h3>Step 3 — Verify Security Configuration</h3>
<br />
Run the following commands to confirm public access is disabled, network rules are set to deny, and the private endpoint provisioned successfully. The failed curl response is expected and confirms the configuration is working correctly. <br/>
<br/>
<img src="https://github.com/user-attachments/assets/a27cb234-d04c-4491-a147-9eb0c8888c45" height="80%" width="80%" alt="VM-NSG Confirmation"/>
<br />
<br />
<img src="https://github.com/user-attachments/assets/c3cc47ca-e355-4a3c-a946-db95b2a34543" height="80%" width="80%" alt="VNET Confirmation"/>
<br />
<br />
<br />
<h3>Step 4 — Create a Blob Container and Test with SAS Token</h3>
<br />
Create a blob container, generate a time-limited SAS token, then use Azure Storage Explorer to upload and download a test file to confirm scoped access works correctly. <br/>
<br/>
<img src="https://github.com/user-attachments/assets/5523f417-455f-456a-aa0f-1dbc0f332a70" height="80%" width="80%" alt="Shared Drive"/>
<br />
<br />
<br />
<h3>Step 5 — Assign a Built-in Azure Policy</h3>
<br />
Navigate to Azure Policy > Definitions, search for "Secure transfer to storage accounts should be enabled", click Assign, set the scope to rg-lab03, and click Review and Create. Wait 15-20 minutes then navigate to rg-lab03 > Policies to review the compliance state.  <br/>
<br/>
<img src="https://github.com/user-attachments/assets/01b51beb-a4e2-402f-ac9b-270d29243c63" height="80%" width="80%" alt="Password Policy GPO Linked to Domain"/>
<br />
<br />
<h3>Step 6 — Cleanup</h3>
<br />
Delete the resource group to remove all provisioned resources and avoid ongoing charges.  <br/>
<br/>
<img src="https://github.com/user-attachments/assets/01b51beb-a4e2-402f-ac9b-270d29243c63" height="80%" width="80%" alt="Password Policy GPO Linked to Domain"/>
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
