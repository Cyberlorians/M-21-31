<details>
<summary><strong>📘 Event Logging Overview</strong></summary>
<p>

### 1. Event Logging Overview

| Field               | Description                                                                                      |
|--------------------|--------------------------------------------------------------------------------------------------|
| **CriticalityID**   | Used as a mapping reference.                                                                      |
| **Function**        | The M2131 Function as defined in the official guidance.                                           |
| **Category**        | Logical grouping within the function.                                                            |
| **Sub-Category**    | Additional filtering within the category.                                                        |
| **Required Data**   | Requirement from Executive Orders.                                                               |
| **Workload**        | Specifies what workload/technology must be enabled for event verification.                       |
| **Table**           | The Log Analytics Workspace table where events are written.                                      |
| **Schema**          | The schema structure of the table.                                                               |
| **Schema Value**    | The specific schema element being validated for the event.                                       |
| **IsCollected**     | User must confirm table collection via the Workload & Table Management form.                     |
| **Event Validated** | User must confirm validation via the Event Queries tab and Sentinel Workbook (if applicable).    |

![Event Logging Form Overview](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp1.png)

---

### 2. Main Form Reference View

This section replicates the data from the main form. It also includes:

- **Reference Content**: Offers descriptions and instructions on how to enable workloads.  
- **History**: A section to log notes, emails, or relevant correspondence.

![Form Reference View](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp2.png)

---

### 3. Table Implementation Status

| Field                 | Description                                                                                      |
|----------------------|--------------------------------------------------------------------------------------------------|
| **Table**            | Used as a mapping reference.                                                                      |
| **Table Implementation** | Automatically updates based on workload and table form.                                       |
| **Implementation Date**  | Automatically updates based on workload and table form.                                       |
| **In Use**           | Indicates if the table is actively in use.                                                       |
| **Connected**        | Auto-adjusts when workload and table are properly linked.                                        |
| **12 Month Retention** | Selection-based; optional setting for compliance.                                              |
| **18 Month Retention** | Selection-based; optional setting for compliance.                                              |

![Table Implementation Status](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp3.png)

---

Select **"+New Storage Location"** and enter where your logs are collected (both hot and cold storage, if applicable).

![New Storage Location](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp4.png)

Once added, both locations will reflect in the interface. However, **you must still update your compliance status manually** if required.

![Storage Locations View](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp5.png)

The **Event Queries** tab will display the `EventKQL`. Once confirmed, you can toggle **Event Validated** to "Yes".

![Event Queries View](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp6.png)

</p>
</details>

---

<details>
<summary><strong>📂 Workload & Table Management</strong></summary>
<p>

This interface mirrors how diagnostic logs (e.g., Entra ID) are enabled in Log Analytics/Sentinel.

1. Select a **workload**.
2. On the right, select the **tables being ingested**.

> ✅ When a table is selected, it will be flagged as "collected"—meaning it's being ingested and is ready to receive validated events.

![Workload Selection](https://github.com/Cyberlorians/M-21-31/blob/main/Images/TableCollection1.png)

Once a table is marked as collected, the **Table Implementation Status** form will **auto-update** with:

- Implementation status  
- Date implemented  
- Connection status

![Auto Update View](https://github.com/Cyberlorians/M-21-31/blob/main/Images/TableCollection2.png)

</p>
</details>

---

<details>
<summary><strong>📑 Event Verification Workbook</strong></summary>
<p>

Use the [M2131-EL-Verification Workbook](https://github.com/Cyberlorians/Workbooks/blob/main/M2131-EL-Verification.json) in your Log Analytics workspace.

1. Import the workbook.  
2. Choose the **Category** and **CriticalityID** to verify.

![Workbook Overview](https://github.com/Cyberlorians/M-21-31/blob/main/Images/workbook1.png)

Once selected, the workbook will:

- Correlate the **CriticalityID**
- Display **KQL artifacts**
- Confirm **Event Verification**

> ⚠️ If no data appears:  
> - Adjust the KQL via the **Log Analytics icon** next to "Event Verification"  
> - Confirm if any relevant events exist for validation

![KQL & Verification](https://github.com/Cyberlorians/M-21-31/blob/main/Images/workbook2.png)

</p>
</details>
