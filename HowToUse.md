<details><summary>Event Logging Overview</summary>
<p>


1 - Event Logging Overview.

| Field             | Description                                                                                      |
|------------------|--------------------------------------------------------------------------------------------------|
| **CriticalityID**   | Used as a mapping reference.                                                                      |
| **Function**        | This is the M2131 Function depicted in their guidance.                                            |
| **Category**        | Filtration within the function.                                                                   |
| **Sub-Category**    | Filtration within the category.                                                                   |
| **Required Data**   | Executive Orders requirement.                                                                     |
| **Workload**        | Depicts what workload/technology is to be enabled for event verification.                         |
| **Table**           | The table that is written to Log Analytics Workspace.                                             |
| **Schema**          | The schema within the table.                                                                      |
| **Schema Value**    | The value which is focused on within the schema for event verification.                           |
| **IsCollected**     | User must verify that the table is being collected via the Workload and Table Management form.    |
| **Event Validated** | User must verify if the event has been verified via the Event Queries tab and Sentinel Workbook (if applicable). |

![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp1.png)

2 - In Overview, the same data is shown from the main form. In addition to, Reference content which will give a reference of what the data is and how to enable the workload. History is used to enter notes, email etc.

![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp2.png)

3 - Table Implementation Status

| Field             | Description                                                                                      |
|------------------|--------------------------------------------------------------------------------------------------|
| **Table**   | Used as a mapping reference.                                                                      |
| **Table Implemenatation**        | Select options at will. This will automatically adjust when workload and table form is updated.|
| **Implementation Date**        | Select options at will. This will automatically adjust when workload and table form is updated.|
| **In Use**    | Select option if table is in use.|
| **Connected**   | Select options at will. This will automatically adjust when workload and table form is updated.|
| **12 Month Retention**        | Select options at will.                        |
| **18 Month Retention**           | Select options at will.                                            |

   
![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp3.png)

Select "+New Storage Location", and enter enter where your logs are collected. For both, hot and cold, if applicable.

![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp4.png)

When added, both locations will refelect but you will still need to update if you are compliant with the mandate.

![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp5.png)

Event queries tab is giving you the EventKQL. Once confirmed, you may select the toggle switch of Event Validated and it will flag to yes.

![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp6.png)

</p>
</details>


<details><summary>Workload & Table Management</summary>
<p>

This is mimicked off how you would view, for example enabling Entra Diagnostic logs to LogA/Sentinel. Select the workload and on the right hand side, select the tables that are being ingested. Note - when selected, the table will flag as collected. What this means is the table is being collected in your logging strategy which are ready to accept "events". 

![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/TableCollection1.png)

Once the box is checked as collected, the Table Implementation Status form will automatically update to Implemented, Date implemented and Connected.

![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/TableCollection2.png)

</p>
</details>

<details><summary>Event Verification Workbook</summary>
<p>

Copy the [M2131-Event-Verfication]() Workbook to your LogA instance. Select The options as shown below. Click on Category and proper CriticalityID that needs to be verified.

![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/workbook1.png)

Once selected, the workbook will correlate the CriticalityID, show the KQL artifacts and prove the Event Verification. IF there is no data. Please adjust the kql with LogA icon next to EVENT VERIFICATION and/or their may not be an event to prove the event.

![](https://github.com/Cyberlorians/M-21-31/blob/main/Images/workbook2.png)

</p>
</details>
