<details><summary>M2131-ICAM-WinEvents - MANDATORY</summary>
<p>
   
**Disclaimer - SecurityEvents tables is used primarily because UEBA leverages only this table.

1. Add Windows Security Events via AMA from Content Hub.
2. Open Windows Security Events via AMA from Data Connectors blade within Sentinel.
3. Click, "Create data collection rule". Enter the name you see as titled.
![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/ICAMWinevent01.png)

5. Add Windows Domain Controllers and Member Servers
![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/ICAMWinevent02.png)

6. Collect "custom" and enter the data located at [M2131-ICAM-WinEvents](https://github.com/Cyberlorians/M-21-31/blob/main/EL0/Identity/M2131-ICAM-WinEvents.md)
![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/ICAMWinevent03.png)

7. Review & Create.   
![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/ICAMWinevent04.png)

9. Review the DCR was created.
![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/ICAMWinevent05.png)
</p>
</details>


<details><summary>M2131-ICAM-EntraConnectAdminActions - If Applicable</summary>
<p>

1. Deploy a [custom template](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/quickstart-create-templates-use-the-portal#edit-and-deploy-the-template)

2. Grab the [M2131-ICAM-EntraConnectAdminActions](https://github.com/Cyberlorians/M-21-31/blob/main/EL0/Identity/M2131-ICAM-EntraConnectAdminActions.json) & paste into the deployment.

3. Configure Project Details as follows
![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131-icam-Entra.png)
   1. Subscription - where the DCR will reside.
   2. Resource Group - where DCR Will reside.
   3. Region - where DCR will reside.
   4. Data Collection Rull Name - will be hardcoded already and aligned to naming scructure.
   5. Location - this is the region of the LogA instance. You can find the exact region under the JSON [resourceId](https://github.com/Cyberlorians/M-21-31/blob/main/Images/LogAResourceId.png) of the LogA workspace.
   6. Workspace Region Id - this is the LogA JSON [resourceId](https://github.com/Cyberlorians/M-21-31/blob/main/Images/LogAResourceId.png) of the LogA workspace.


</p>
</details>

<details><summary>M2131-ICAM-AzureADPasswordProtection - If Applicable</summary>
<p>

1. Deploy a [custom template](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/quickstart-create-templates-use-the-portal#edit-and-deploy-the-template)

2. Grab the [M2131-ICAM-AzureADPasswordProtection](https://github.com/Cyberlorians/M-21-31/blob/main/EL0/Identity/M2131-ICAM-AzureADPasswordProtection.json) & paste into the deployment.

3. Configure Project Details as follows
![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131-ICAM-Entra.png)
   1. Subscription - where the DCR will reside.
   2. Resource Group - where DCR Will reside.
   3. Region - where DCR will reside.
   4. Data Collection Rull Name - will be hardcoded already and aligned to naming scructure.
   5. Location - this is the region of the LogA instance. You can find the exact region under the JSON [resourceId](https://github.com/Cyberlorians/M-21-31/blob/main/Images/LogAResourceId.png) of the LogA workspace.
   6. Workspace Region Id - this is the LogA JSON [resourceId](https://github.com/Cyberlorians/M-21-31/blob/main/Images/LogAResourceId.png) of the LogA workspace.
</p>
</details>
