# Why Use This Workbook

This workbook was purpose-built to help agencies, defenders, and compliance leads measure their telemetry maturity against the M-21-31 logging requirements. Rather than abstract guidance, it provides actionable queries and validation logic directly aligned to each audit category.

---

## 📌 Core Benefits

### ✅ Direct Mapping to M-21-31 Logging Categories
Each section of this workbook aligns to a defined control or event logging requirement in the M-21-31 memorandum. This helps ensure federal agencies are collecting data that supports Zero Trust, forensics, and rapid incident response.

### ✅ Visual Validation
With built-in checks using KQL queries across Microsoft Defender, Sentinel, and other data sources, the workbook provides **real-time validation** of whether the required logs exist — and from which systems.

### ✅ Multi-Workload Coverage
Supports validation across:
- Microsoft Defender for Endpoint (MDE)
- Microsoft Defender for Office (MDO)
- Azure AD / Entra ID
- Windows Event Logs
- Syslog / Linux
- Third-party SaaS sources (custom sections)

### ✅ Reduces Guesswork and Manual Review
By automating validation through queries, teams can move away from PDF checklists or spreadsheets. Instead, they can immediately see what’s missing or misaligned.

---

## 🎯 Use Cases

- 📊 **Compliance Reviews**: Prepare for CDM, IGCE, or internal logging assessments.
- 🛡 **Security Readiness**: Ensure you have telemetry to support detection, containment, and investigation.
- 🔁 **Cross-Team Collaboration**: Helps bridge compliance, SOC, and ITOps teams with clear, aligned expectations.
- ⚙️ **Audit & Continuous Monitoring**: Integrate into dashboards or executive briefings to show ongoing maturity progress.

---

## 📁 What This Is Not

- ❌ This is not a logging policy generator
- ❌ It does not replace agency-specific logging guides
- ❌ It is not exclusive to Sentinel — the queries can be ported to other platforms that support KQL or structured log validation

---

## 🚀 Get Started

Use this workbook in combination with your agency’s log ingestion sources and data connectors. Populate the validation queries and review the results to begin mapping your actual telemetry to the expected M-21-31 standard.

For how-to guidance, refer to: [`HowToUse.md`](./HowToUse.md)
