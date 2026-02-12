```
source
| extend CAPResult_CF = extract_all(@"(\{[^{}]*""result"":""(success|failure)""[^{}]*\})", tostring(ConditionalAccessPolicies))
| project-away ConditionalAccessPolicies
| where not(isempty(CAPResult_CF))
```
# AADNonInteractiveUserSignInLogs — DCR Transform

## TL;DR
Strip Conditional Access noise from `AADNonInteractiveUserSignInLogs` using a DCR transform. **~90% ingestion cost reduction.**

## Why This Table Is Expensive
- Non-interactive sign-ins (token refreshes, background app calls) **constantly re-evaluate CA policies**
- Each log carries a massive `ConditionalAccessPolicies` JSON blob with dozens of policy objects
- Most results are `notApplied` / `notEnabled` — zero detection value
- This table is often a **top 3 cost driver** in Sentinel workspaces

## The Transform
```kql
source
| extend CAPResult_CF = extract_all(@"(\{[^{}]*""result"":""(success|failure)""[^{}]*\})", tostring(ConditionalAccessPolicies))
| project-away ConditionalAccessPolicies
| where not(isempty(CAPResult_CF))
```

## What It Does
- **`extract_all`** — Keeps only CA policy evaluations with `success` or `failure` results
- **`project-away`** — Drops the bloated raw JSON column, replaced by the filtered extract
- **`where not(isempty(...))`** — Drops rows where no CA policy actually fired

## What You Keep vs. Drop

| Keep | Drop |
|------|------|
| CA policy **success** (allowed) | `notApplied` results |
| CA policy **failure** (blocked) | `notEnabled` results |
| Compact extracted results | Full JSON policy blob |

## Cost Impact
- **~90% reduction** in ingestion volume on this table
- Bulk of non-interactive logs are redundant CA re-evaluations with `notApplied` against dozens of policies
- Only actionable policy decisions are retained

## Detection Value
- Every blocked sign-in (CA failure) is preserved — critical for security monitoring
- Every allowed sign-in through CA (success) is preserved — needed for investigation
- Zero loss of detection fidelity for SOC use cases

## If You Need the Raw Data
Send unfiltered logs to a **Basic tier table** or **Storage Account** for compliance at a fraction of the cost.

// Before CAP removed
AADNonInteractiveUserSignInLogs | summarize MessageCount = count(), DataIngestedGB = sum(_BilledSize) / 1024 / 1024 / 1024
 
// CAP filtered out to only allow success
AADNonInteractiveUserSignInLogs | extend ConditionalAccessPolicies_CF = extract_all(@"(\{[^{}]*""result"":""success""[^{}]*\})",ConditionalAccessPolicies) | project-away ConditionalAccessPolicies | where not(isempty(ConditionalAccessPolicies_CF)) | summarize MessageCount = count(), DataIngestedGB = sum(_BilledSize) / 1024 / 1024 / 1024
