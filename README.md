# biostar2-ad-credential-exposure
CVE write-up for Active Directory credential exposure vulnerability in Suprema BioStar 2
# CVE-Pending – Suprema BioStar 2 Active Directory Credential Exposure

## Summary

A sensitive information disclosure vulnerability exists in Suprema BioStar 2 due to improper handling of Active Directory integration settings. The backend API endpoint `/api/v2/setting/adserversetting` returns Active Directory bind account credentials in plaintext.

## Technical Details

Although the password field is masked in the administrative interface, authenticated requests to the backend API disclose the full unencrypted password along with LDAP configuration parameters, including disabled SSL communication.

This exposure allows retrieval of domain service account credentials used for directory synchronization.

## Impact

An authenticated attacker may leverage the disclosed credentials to:

- Perform LDAP authentication against Active Directory  
- Enumerate domain users, groups, and organizational units  
- Conduct internal reconnaissance  
- Perform lateral movement across domain-connected systems  
- Potentially escalate privileges depending on account permissions  

## Vulnerability Type

- Sensitive Information Disclosure  
- Credential Exposure  
- Security Misconfiguration  

## Attack Vector

Remote / Authenticated / Low Complexity  

## Credit

Abdullah Alannaz - Security Researcher
