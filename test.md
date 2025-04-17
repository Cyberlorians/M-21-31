<details>
<summary><strong>📘 Event Logging Overview</strong></summary>
<p>

---

### 🧾 Event Logging Form

This is the main data-entry interface where users define and track logging requirements for specific workloads. It captures mapping details required by the M-21-31 Executive Order.

| Field               | Description                                                                                      |
|--------------------|--------------------------------------------------------------------------------------------------|
| **CriticalityID**   | Mapping identifier based on log importance/urgency.                                              |
| **Function**        | Corresponds to M-21-31 logging functions as outlined in the official guidance.                   |
| **Category**        | Logical grouping of logging requirements.                                                        |
| **Sub-Category**    | Further refinement of the category to pinpoint scope.                                            |
| **Required Data**   | Defines the data required under M-21-31 or EO 14028.                                             |
| **Workload**        | Specifies which Microsoft service or technology is responsible for generating the log.          |
| **Table**           | The Log Analytics Workspace table where the data is collected.                                   |
| **Schema**          | Structure of the expected data within the selected table.                                        |
| **Schema Value**    | The specific log field to be validated.                                                          |
| **IsCollected**     | Indicates if the table is actively being ingested (validated through Table Management view).     |
| **Event Validated** | Confirmed via the Event Queries tab and Microsoft Sentinel Workbook (if applicable).             |

![Event Logging Form](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp1.png)

---

### 📖 Reference View & Notes

This view replicates the main form’s data but includes:

- **Reference Content**: How-to instructions and contextual metadata for each workload  
- **History Section**: Notes, comments, emails, or supporting artifacts

![Reference View](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp2.png)

---

### 📈 Table Implementation Status

Tracks whether event tables have been implemented and aligned with retention standards.

| Field                    | Description                                                                                  |
|--------------------------|----------------------------------------------------------------------------------------------|
| **Table**                | Table name in Log Analytics Workspace                                                        |
| **Table Implementation** | Updated dynamically based on selections in Workload & Table Management                       |
| **Implementation Date**  | Auto-populated upon table confirmation                                                       |
| **In Use**               | Toggle to indicate whether this table is actively used                                       |
| **Connected**            | Reflects current linkage status between workload and table                                   |
| **12 Month Retention**   | Optional selection for retention verification                                                |
| **18 Month Retention**   | Optional selection for extended retention compliance                                         |

![Table Implementation Status](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp3.png)

---

### 🗄️ Storage Configuration

Click **"+New Storage Location"** to specify your log collection destinations (e.g., hot or cold storage). This supports visibility into log flow and physical storage compliance.

![Add Storage Location](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp4.png)

Once added, the locations will appear in the interface. **Manual updates are required** to reflect current compliance standing.

![Storage Location View](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp5.png)

---

### 🧪 Event Queries Tab

The **Event Queries** tab provides the actual KQL used for validation. Once confirmed through Sentinel or manual review, toggle **Event Validated** to "Yes".

![Event Queries](https://github.com/Cyberlorians/M-21-31/blob/main/Images/m2131powerapp6.png)

</p>
</details>
