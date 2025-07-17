
```
 "xPathQueries": [
                        "Security!*[System[(EventID=4608) or (EventID=4609) or (EventID=4624) or (EventID=4625) or (EventID=4634) or (EventID=4647) or (EventID=4656) or (EventID=4657) or (EventID=4658) or (EventID=4660) or (EventID=4663) or (EventID=4673) or (EventID=4674) or (EventID=4685) or (EventID=4778)]]",
                        "Security!*[System[(EventID=4985) or (EventID=5140) or (EventID=5142) or (EventID=5143) or (EventID=5144) or (EventID=5145) or (EventID=5168)]]",
                        "Security!*[System[(EventID=4985) or (EventID=5140) or (EventID=5142) or (EventID=5143) or (EventID=5144) or (EventID=5145) or (EventID=5168) or (EventID=1104)]]",
                        "Security!*[System[(EventID=4985) or (EventID=5140) or (EventID=5142) or (EventID=5143) or (EventID=5144) or (EventID=5145) or (EventID=5168) or (EventID=1104) or (EventID=4660)]]"
                    ]
```

# GPO Path Mapping for Event IDs

Below is a breakdown of each Event ID’s GPO path, organized by where the audit policy should be applied.

---

## Member-Server GPO Paths

| Event ID(s)                          | GPO Path                                                                                                                                                                                                                  |
|--------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **1100, 1102, 1104, 1105, 1108**     | Computer Configuration → Policies → Windows Settings → Security Settings → **Advanced Audit Policy Configuration** → **System** → Audit Other System Events (Success)                                                      |
| **4624**                             | … → **Logon/Logoff** → Audit Logon (Success)                                                                                                                                                                              |
| **4625**                             | … → **Logon/Logoff** → Audit Logon (Failure)                                                                                                                                                                              |
| **4634, 4647**                       | … → **Logon/Logoff** → Audit Logoff (Success)                                                                                                                                                                             |
| **4648**                             | … → **Logon/Logoff** → Audit Logon (Success)                                                                                                                                                                              |
| **4656**                             | … → **Object Access** → Audit File System (Success)<br/>… → **Object Access** → Audit Registry (Success)                                                                                                                   |
| **4657**                             | … → **Object Access** → Audit Registry (Success)                                                                                                                                                                          |
| **4658**                             | … → **Object Access** → Audit Handle Manipulation (Success)                                                                                                                                                                |
| **4660**                             | … → **Object Access** → Audit File System (Success)                                                                                                                                                                       |
| **4663**                             | … → **Object Access** → Audit File System (Success, Failure)<br/>… → **Object Access** → Audit Registry (Success, Failure)                                                                                                  |
| **4670**                             | … → **Object Access** → Audit File System (Success)<br/>… → **Object Access** → Audit Registry (Success)<br/>… → **Policy Change** → Audit Authentication Policy Change (Success)<br/>… → **Policy Change** → Audit Authorization Policy Change (Success) |
| **4720, 4723, 4724, 4738**           | … → **Account Management** → Audit User Account Management (Success, Failure)                                                                                                                                             |
| **4728, 4729, 4732, 4756**           | … → **Account Management** → Audit Security Group Management (Success, Failure)                                                                                                                                            |
| **4907**                             | … → **Policy Change** → Audit Policy Change (Success)                                                                                                                                                                     |
| **4985**                             | … → **Object Access** → Audit File System (Success)<br/>… → **Privilege Use** → Audit Non Sensitive Privilege Use (Success)<br/>… → **Privilege Use** → Audit Other Privilege Use Events (Success)<br/>… → **Privilege Use** → Audit Sensitive Privilege Use (Success) |
| **5140, 5142, 5143, 5144**           | … → **Object Access** → Audit File Share (Success, Failure)                                                                                                                                                               |
| **5145**                             | … → **Object Access** → Audit Detailed File Share (Success, Failure)                                                                                                                                                      |
| **6416**                             | … → **Object Access** → Audit Removable Storage (Success)                                                                                                                                                                 |

---

## Domain-Controller GPO Paths

| Event ID(s)               | GPO Path                                                                                                                                                                                                            |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **4726**                  | Computer Configuration → Policies → Windows Settings → Security Settings → **Advanced Audit Policy Configuration** → **DS Access** → Audit Directory Service Changes (Success, Failure)                       |
| **5136, 5137**            | … → **DS Access** → Audit Directory Service Changes (Success)                                                                                                                                                |
| **4768**                  | … → **Account Logon** → Audit Kerberos Authentication Service (Success, Failure)  _(enable on all domain controllers)_                                                                                       |
| **4771**                  | … → **Account Logon** → Audit Kerberos Authentication Service (Failure)                                                                                                                                      |
| **4776**                  | … → **Account Logon** → Audit Credential Validation (Failure)                                                                                                                                                |
| **4887**                  | On the CA(s): enable the **Issue and manage certificate requests** audit setting, and enable the **Certificate Services** subcategory via `auditpol`                                                          |
| **5168**                  | Local Policies → Security Options → Network security: Restrict NTLM: Audit NTLM authentication in this domain                                                                                                  |
| **4672**                  | … → **Logon/Logoff** → Audit Special Logon (Success)                                                                                                                                                         |
| **4673, 4674**            | … → **Privilege Use** → Audit Sensitive Privilege Use (Success)                                                                                                                                                |

---

> **Notes**  
> - All of the “Account Management,” “Logon/Logoff,” “Object Access,” “Policy Change” and “DS Access” settings live under **Computer Configuration → Policies → Windows Settings → Security Settings → Advanced Audit Policy Configuration** in your GPO.  
> - Events tied to AD–DS or Kerberos (4726, 5136/5137, 4768) should be configured in a GPO linked to your **Domain Controllers** OU.  
> - The rest should be applied to your **Member Servers** (and workstations) via a separate GPO.  
