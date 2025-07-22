# Why Use This Workbook

This workbook is built to operationalize the M-21-31 event logging maturity model — transforming vague guidance into concrete, query-driven validation of telemetry coverage. It enables security teams, auditors, and engineers to prove what’s really being logged, where it’s flowing, and whether it can be used for detection, response, and compliance.

---

## 📌 Core Benefits

### ✅ Direct Mapping to M-21-31 Logging Categories
Each workbook section maps to a specific logging requirement from the M-21-31 memorandum. You’re not guessing — you’re validating what exists and pinpointing gaps.

### ✅ Real-Time Telemetry Validation
Rather than checklists or theoretical recommendations, this workbook uses live KQL queries against your Microsoft Defender and Sentinel data to confirm whether essential log types are being collected.

### ✅ Broad Workload Coverage
Supports validation across:
- Microsoft Defender for Endpoint (MDE)
- Microsoft Defender for Office (MDO)
- Entra ID (Azure AD)
- Windows Security Events
- Linux Syslog (auditd/local3)
- Third-party SaaS (via Sentinel connectors)

### ✅ Designed for Collaboration
Whether you're in the SOC, compliance, or infrastructure teams, this workbook gives you a shared, structured lens to evaluate logging posture in a Zero Trust world.

---

## 🎯 Use Case Example – Identity: Entra ID User Creation

This example tracks account creation activity in Entra ID (`Add user` operations via the AuditLogs table).

### 📂 Mapping Snapshot:
- **Category:** Identity & Credential Management  
- **Subcategory:** Account → Account Creation  
- **Data Source:** Entra ID  
- **Table:** AuditLogs  
- **OperationName:** Add user  
- **Docs:**  
  - [How to Integrate Audit Logs](https://learn.microsoft.com/en-us/entra/identity/monitoring-health/howto-integrate-activity-logs-with-azure-monitor-logs)  
  - [Audit Log Concepts](https://learn.microsoft.com/en-us/entra/identity/monitoring-health/concept-audit-logs)

---

### 🔐 Why This Is Critical

#### 🛡 Identity Visibility
- Confirms whether Entra is emitting logs for user creation — a must-have for both Zero Trust and insider threat mitigation.
- Reveals which admin or app created the account and whether it succeeded or failed.

#### 🔎 Threat Hunting
- Enables rapid pivoting by IP, actor, or target account.
- Can be chained with role assignments or sign-ins to investigate suspicious user lifecycles.

#### 🔥 DFIR Readiness
- During an incident, quickly determine if shadow accounts were created.
- Establish intent and actor type (sync process vs. interactive user vs. app).

#### 📋 M-21-31 Compliance
- Satisfies event logging requirements around account provisioning.
- Validates not just that logs exist — but that they are parsed and queryable.

---

### 🧠 Live Query Example (Workbook Embedded):

```kql
// Objective: Detects new user creation events in Entra ID and allows for targeted filtering by initiator or target UPN.

let TargetedUserUPNs = dynamic([]); // Example: ["user1@domain.com"]
let InitiatorUPNs = dynamic([]);    // Example: ["admin@domain.com"]

AuditLogs
| where TimeGenerated > ago(30d)
| where OperationName == "Add user"
| extend InitiatorInfo = todynamic(InitiatedBy)
| extend TargetInfo = todynamic(TargetResources)[0]
| extend
    Status = Result,
    FailureReason = tostring(ResultSignature),
    InitiatorType = case(
        tostring(InitiatorInfo.user.userPrincipalName) has_cs "Sync", "Sync Process",
        isnotempty(InitiatorInfo.user.userPrincipalName), "Interactive User",
        isnotempty(InitiatorInfo.app.displayName), "Application",
        "Other"
    ),
    Initiator = coalesce(
        tostring(InitiatorInfo.user.userPrincipalName),
        tostring(InitiatorInfo.app.displayName)
    ),
    InitiatorIpAddress = tostring(InitiatorInfo.user.ipAddress),
    TargetUserUPN = tostring(TargetInfo.userPrincipalName),
    TargetUserID = tostring(TargetInfo.id)
| where (array_length(TargetedUserUPNs) == 0 or TargetUserUPN in (TargetedUserUPNs))
| where (array_length(InitiatorUPNs) == 0 or Initiator in (InitiatorUPNs))
| distinct TimeGenerated, Status, FailureReason, InitiatorType, Initiator, InitiatorIpAddress, TargetUserUPN, TargetUserID
| sort by TimeGenerated desc
| take 50
