<details>
<summary><strong>📘 Event Logging Overview</strong></summary>
<p>

### Event Logging Form

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

### Main Form Reference View

This section replicates the data from the main form. It also includes:

- **Reference Content**: Offers descriptions and instructions on how to enable workloads.  
- **History**: A section to log notes, emails, or relevant correspondence.

![Form Reference View](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp2.png)

---

### Table Implementation Status

| Field                   | Description                                                                                      |
|------------------------|--------------------------------------------------------------------------------------------------|
| **Table**              | Used as a mapping reference.                                                                      |
| **Table Implementation** | Automatically updates based on workload and table form.                                         |
| **Implementation Date**  | Automatically updates based on workload and table form.                                         |
| **In Use**             | Indicates if the table is actively in use.                                                       |
| **Connected**          | Auto-adjusts when workload and table are properly linked.                                        |
| **12 Month Retention** | Selection-based; optional setting for compliance.                                                |
| **18 Month Retention** | Selection-based; optional setting for compliance.                                                |

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
