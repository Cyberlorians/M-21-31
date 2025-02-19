```
source
| extend CAPResult_CF = extract_all(@"(\{[^{}]*""result"":""(success|failure)""[^{}]*\})", tostring(ConditionalAccessPolicies))
| project-away ConditionalAccessPolicies
| where not(isempty(CAPResult_CF))
```
