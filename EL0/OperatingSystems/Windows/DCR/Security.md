Below are the EventIDs mapped for interation #1 under User and Access Administration. 
```
 "xPathQueries": [
                        "Security!*[System[(EventID=4608) or (EventID=4609) or (EventID=4624) or (EventID=4625) or (EventID=4634) or (EventID=4647) or (EventID=4656) or (EventID=4657) or (EventID=4658) or (EventID=4660) or (EventID=4663) or (EventID=4673) or (EventID=4674) or (EventID=4685) or (EventID=4778)]]",
                        "Security!*[System[(EventID=4985) or (EventID=5140) or (EventID=5142) or (EventID=5143) or (EventID=5144) or (EventID=5145) or (EventID=5168)]]",
                        "Security!*[System[(EventID=4985) or (EventID=5140) or (EventID=5142) or (EventID=5143) or (EventID=5144) or (EventID=5145) or (EventID=5168) or (EventID=1104)]]",
                        "Security!*[System[(EventID=4985) or (EventID=5140) or (EventID=5142) or (EventID=5143) or (EventID=5144) or (EventID=5145) or (EventID=5168) or (EventID=1104) or (EventID=4660)]]"
                    ]
```

What is recommended is to DEPLOY the common Security Event IDs with Sentinel and after deployment adjust the DCR rule to add the above in combination with common. Below is Common SecIDs & M2131 User Access Category.

```
{
    "xPathQueries": [
        "Security!*[System[((EventID=1) or (EventID=299) or (EventID=300) or (EventID=324) or (EventID=340) or (EventID=403) or (EventID=404) or (EventID=410) or (EventID=411) or (EventID=412) or (EventID=413) or (EventID=431) or (EventID=500) or (EventID=501) or (EventID=1100))]]",
        "Security!*[System[((EventID=1102) or (EventID=1107) or (EventID=1108) or (EventID=4608) or (EventID=4610) or (EventID=4611) or (EventID=4614) or (EventID=4622) or (EventID=4624) or (EventID=4625) or (EventID=4634) or (EventID=4647) or (EventID=4648) or (EventID=4649) or (EventID=4657))]]",
        "Security!*[System[((EventID=4661) or (EventID=4662) or (EventID=4663) or (EventID=4665) or (EventID=4666) or (EventID=4667) or (EventID=4670) or (EventID=4672) or (EventID=4673) or (EventID=4674) or (EventID=4675) or (EventID=4688) or (EventID=4689) or (EventID=4697) or (EventID=4700))]]",
        "Security!*[System[((EventID=4702) or (EventID=4704) or (EventID=4705) or (EventID=4716) or (EventID=4717) or (EventID=4718) or (EventID=4719) or (EventID=4720) or (EventID=4722) or (EventID=4723) or (EventID=4724) or (EventID=4725) or (EventID=4726) or (EventID=4727) or (EventID=4728))]]",
        "Security!*[System[((EventID=4729) or (EventID=4732) or (EventID=4733) or (EventID=4735) or (EventID=4737) or (EventID=4738) or (EventID=4739) or (EventID=4740) or (EventID=4742) or (EventID=4744) or (EventID=4745) or (EventID=4746) or (EventID=4750) or (EventID=4751) or (EventID=4752))]]",
        "Security!*[System[((EventID=4754) or (EventID=4755) or (EventID=4756) or (EventID=4757) or (EventID=4760) or (EventID=4761) or (EventID=4762) or (EventID=4764) or (EventID=4767) or (EventID=4768) or (EventID=4771) or (EventID=4774) or (EventID=4778) or (EventID=4779) or (EventID=4781))]]",
        "Security!*[System[((EventID=4793) or (EventID=4797) or (EventID=4798) or (EventID=4799) or (EventID=4800) or (EventID=4801) or (EventID=4802) or (EventID=4803) or (EventID=4825) or (EventID=4826) or (EventID=4870) or (EventID=4886) or (EventID=4887) or (EventID=4888) or (EventID=4893))]]",
        "Security!*[System[((EventID=4898) or (EventID=4902) or (EventID=4904) or (EventID=4905) or (EventID=4907) or (EventID=4931) or (EventID=4932) or (EventID=4933) or (EventID=4946) or (EventID=4948) or (EventID=4956) or (EventID=4985) or (EventID=5024) or (EventID=5033) or (EventID=5059))]]",
        "Security!*[System[((EventID=5136) or (EventID=5137) or (EventID=5140) or (EventID=5145) or (EventID=5632) or (EventID=6144) or (EventID=6145) or (EventID=6272) or (EventID=6273) or (EventID=6278) or (EventID=6416) or (EventID=6423) or (EventID=6424) or (EventID=8001) or (EventID=8002))]]",
        "Security!*[System[((EventID=8003) or (EventID=8004) or (EventID=8005) or (EventID=8006) or (EventID=8007) or (EventID=8222) or (EventID=26401) or (EventID=30004))]]"
    ]
}
```

# GPO Path Mapping for Event IDs

> **Note:** You may already have these audit policies configured according to your organization’s hardening guidelines (e.g., NIST, DoD, or other industry standards). Please review your current logging configuration and add any missing settings.

> **Notes**
> - All of the “Account Management,” “Logon/Logoff,” “Object Access,” “Policy Change,” and “DS Access” settings live under:  
>   **Computer Configuration → Policies → Windows Settings → Security Settings → Advanced Audit Policy Configuration**  
> - Events tied to AD DS or Kerberos (4726, 5136/5137, 4768) should be configured in a GPO linked to your **Domain Controllers** OU.  
> - All other events should be applied to your **Member Servers** (and workstations) via a separate GPO.

---

## Member-Server GPO Paths

| Event ID(s)                      | GPO Path                                                                                                                                                                                                                                       |
|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **1100, 1102, 1104, 1105, 1108** | Computer Configuration → Policies → Windows Settings → Security Settings → **Advanced Audit Policy Configuration** → **System** → Audit Other System Events (Success)                                                                            |
| **4624**                         | … → **Logon/Logoff** → Audit Logon (Success)                                                                                                                                                                                                   |
| **4625**                         | … → **Logon/Logoff** → Audit Logon (Failure)                                                                                                                                                                                                   |
| **4634, 4647**                   | … → **Logon/Logoff** → Audit Logoff (Success)                                                                                                                                                                                                  |
| **4648**                         | … → **Logon/Logoff** → Audit Logon (Success)                                                                                                                                                                                                   |
| **4656**                         | … → **Object Access** → Audit File System (Success)<br/>… → **Object Access** → Audit Registry (Success)                                                                                                                                        |
| **4657**                         | … → **Object Access** → Audit Registry (Success)                                                                                                                                                                                               |
| **4658**                         | … → **Object Access** → Audit Handle Manipulation (Success)                                                                                                                                                                                     |
| **4660**                         | … → **Object Access** → Audit File System (Success)                                                                                                                                                                                            |
| **4663**                         | … → **Object Access** → Audit File System (Success, Failure)<br/>… → **Object Access** → Audit Registry (Success, Failure)                                                                                                                     |
| **4670**                         | … → **Object Access** → Audit File System (Success)<br/>… → **Object Access** → Audit Registry (Success)<br/>… → **Policy Change** → Audit Authentication Policy Change (Success)<br/>… → **Policy Change** → Audit Authorization Policy Change (Success) |
| **4720, 4723, 4724, 4738**       | … → **Account Management** → Audit User Account Management (Success, Failure)                                                                                                                                                                  |
| **4728, 4729, 4732, 4756**       | … → **Account Management** → Audit Security Group Management (Success, Failure)                                                                                                                                                               |
| **4907**                         | … → **Policy Change** → Audit Policy Change (Success)                                                                                                                                                                                          |
| **4985**                         | … → **Object Access** → Audit File System (Success)<br/>… → **Privilege Use** → Audit Non Sensitive Privilege Use (Success)<br/>… → **Privilege Use** → Audit Other Privilege Use Events (Success)<br/>… → **Privilege Use** → Audit Sensitive Privilege Use (Success) |
| **5140, 5142, 5143, 5144**       | … → **Object Access** → Audit File Share (Success, Failure)                                                                                                                                                                                    |
| **5145**                         | … → **Object Access** → Audit Detailed File Share (Success, Failure)                                                                                                                                                                           |
| **6416**                         | … → **Object Access** → Audit Removable Storage (Success)                                                                                                                                                                                      |

---

## Domain-Controller GPO Paths

| Event ID(s)        | GPO Path                                                                                                                                                                                                                  |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **4726**           | Computer Configuration → Policies → Windows Settings → Security Settings → **Advanced Audit Policy Configuration** → **DS Access** → Audit Directory Service Changes (Success, Failure)                                  |
| **5136, 5137**     | … → **DS Access** → Audit Directory Service Changes (Success)                                                                                                                                                              |
| **4768**           | … → **Account Logon** → Audit Kerberos Authentication Service (Success, Failure) _(enable on all domain controllers)_                                                                                                     |
| **4771**           | … → **Account Logon** → Audit Kerberos Authentication Service (Failure)                                                                                                                                                    |
| **4776**           | … → **Account Logon** → Audit Credential Validation (Failure)                                                                                                                                                              |
| **4887**           | On the CA(s): enable the **Issue and manage certificate requests** audit setting, and enable the **Certificate Services** subcategory via `auditpol`                                                                     |
| **5168**           | Local Policies → Security Options → Network security: Restrict NTLM: Audit NTLM authentication in this domain                                                                                                              |
| **4672**           | … → **Logon/Logoff** → Audit Special Logon (Success)                                                                                                                                                                       |
| **4673, 4674**     | … → **Privilege Use** → Audit Sensitive Privilege Use (Success)                                                                                                                                                            |
