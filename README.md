# biostar2-ad-credential-exposure
CVE write-up for Active Directory credential exposure vulnerability in Suprema BioStar 2
# CVE-Pending – BioStar 2 Active Directory Credential Exposure

## Description
Suprema BioStar 2 exposes Active Directory bind credentials in plaintext via the backend API endpoint `/api/v2/setting/adserversetting`.

## Impact
Authenticated attackers can obtain domain credentials, perform LDAP authentication, enumerate users and groups, and potentially conduct lateral movement.

## Credit
Abdullah Alannaz
