<details>
<summary><strong>📘 Event Logging Overview</strong></summary>
<p>

---

### 🧾 Event Logging Form

The **Event Logging Form** is the primary interface used to define and track logging requirements for specific workloads. This form captures all necessary mapping details aligned with **M-21-31 Executive Order** and helps users ensure that event logs meet the required standards.

| **Field**            | **Description**                                                                                   |
|----------------------|---------------------------------------------------------------------------------------------------|
| **CriticalityID**     | Mapping identifier based on log importance and urgency as defined in the M-21-31 guidelines.      |
| **Function**          | Defines the M-21-31 logging functions as specified in the official guidance.                      |
| **Category**          | Logical grouping of logging requirements for better organization and management.                 |
| **Sub-Category**      | Further refinement of the category to ensure precise mapping.                                     |
| **Required Data**     | Specifies the data required to be collected, aligned with **M-21-31** or **EO 14028**.            |
| **Workload**          | Identifies the Microsoft service or technology responsible for generating the log data.           |
| **Table**             | Denotes the Log Analytics Workspace table where the event data is collected.                     |
| **Schema**            | Describes the expected structure of the data within the specified table.                          |
| **Schema Value**      | The specific schema field that must be validated to confirm event logging.                        |
| **IsCollected**       | Indicates whether the event table is actively being ingested (verified via Table Management form).|
| **Event Validated**   | Confirms event validation, performed via the **Event Queries** tab and **Microsoft Sentinel Workbook**. |

![Event Logging Form](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp1.png)

---

### 📖 Reference View & Notes

The **Reference View** replicates the data found in the main form and serves as a useful resource for users. It includes:

- **Reference Content**: Clear instructions and contextual metadata for each workload, ensuring easy implementation.
- **History Section**: A place for logging notes, email exchanges, or any other relevant communications.

![Reference View](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp2.png)

---

### 📈 Table Implementation Status

The **Table Implementation Status** provides real-time updates on whether event tables are fully implemented and compliant with retention standards.

| **Field**                | **Description**                                                                                     |
|--------------------------|-----------------------------------------------------------------------------------------------------|
| **Table**                | The name of the table within **Log Analytics Workspace** that logs events.                         |
| **Table Implementation** | Automatically updates based on workload and table selections in the **Workload & Table Management** form. |
| **Implementation Date**  | Date auto-populated once the table is confirmed as implemented.                                      |
| **In Use**               | Indicates whether the table is actively being used to collect events.                              |
| **Connected**            | Reflects the linkage status between the workload and the event table.                              |
| **12 Month Retention**   | Optionally mark if logs should be retained for a 12-month period.                                  |
| **18 Month Retention**   | Optionally mark if logs should be retained for an 18-month period.                                 |

![Table Implementation Status](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp3.png)

---

### 🗄️ Storage Configuration

To manage **storage locations**, simply click on **"+New Storage Location"**. Here you can specify the locations where your logs are being collected, whether in **hot** or **cold storage**, ensuring proper visibility and compliance.

![Add Storage Location](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp4.png)

Once added, both **hot** and **cold** storage locations will be visible in the interface. **Note:** Manual updates are required to reflect your current compliance status.

![Storage Location View](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp5.png)

---

### 🧪 Event Queries Tab

The **Event Queries Tab** is where you confirm the actual **KQL queries** used for event validation. This tab ensures that the events collected meet M-21-31 standards.

1. **Select** the appropriate **CriticalityID** and **Category**.
2. **Review the KQL** queries and ensure the events are being logged correctly.
3. Once verified through **Microsoft Sentinel**, **toggle** the **Event Validated** status to **"Yes"** to confirm that the events are logged and validated.

![Event Queries](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp6.png)

---

### 📂 Workload & Table Management

This interface mirrors how diagnostic logs (e.g., Entra ID) are enabled in **Log Analytics** or **Microsoft Sentinel**.

1. **Select a Workload**: Choose the specific workload that you are tracking (e.g., Entra ID).
2. **Select the Tables**: Choose the tables that will be used for logging events and verify that they are properly ingested.

> ✅ When a table is selected, it will be flagged as **"collected"**—indicating that it's actively receiving data and is ready to be validated for event logging.

![Workload Selection](https://github.com/Cyberlorians/M-21-31/blob/main/Images/TableCollection1.png)

Once a table is marked as **collected**, the **Table Implementation Status** form will **auto-update** to reflect:

- **Implementation status**  
- **Date implemented**  
- **Connection status**  

![Auto Update View](https://github.com/Cyberlorians/M-21-31/blob/main/Images/TableCollection2.png)

---

### 📑 Event Verification Workbook

The **[M-21-31 Event Verification Workbook](https://github.com/Cyberlorians/Workbooks/blob/main/M2131-EL-Verification.json)** is designed to be used within **Microsoft Sentinel** or **Log Analytics** to confirm that event logs are being properly collected and meet the necessary criteria.

1. **Import the Workbook**: Add the workbook to your **Log Analytics** workspace.
2. **Choose the Category and CriticalityID** to match the events you wish to verify.

![Workbook Overview](https://github.com/Cyberlorians/M-21-31/blob/main/Images/workbook1.png)

Once the correct **Category** and **CriticalityID** are selected, the workbook will:

- **Correlate the CriticalityID** with the logs in your system
- **Display KQL artifacts** used for event validation
- **Confirm event verification**, indicating whether the expected events are present in your data

> ⚠️ If no data appears:  
> - **Adjust the KQL** via the **Log Analytics icon** next to "Event Verification."  
> - Ensure that **valid events** are available for validation.

![KQL & Verification](https://github.com/Cyberlorians/M-21-31/blob/main/Images/workbook2.png)

</p>
</details>
