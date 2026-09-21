# Remediating-Cloud-Storage-Vulnerabilities-with-Security-Command-Center
# Remediating Cloud Storage Vulnerabilities with Security Command Center

A hands-on Google Cloud lab where I played the role of a junior cloud security analyst at a fictional bank, finding and fixing a misconfigured Cloud Storage bucket using Security Command Center (SCC).

## Scenario
A storage bucket containing sensitive documents was flagged as misconfigured. My job was to find the exact issues, fix them, and confirm the fix with a compliance report.

## What I did

### 1. Identified the vulnerabilities
Used Security Command Center's Vulnerabilities page to find two active findings on the bucket:
- **Public bucket ACL** (high risk) — the bucket was readable by anyone on the internet via `allUsers`
- **Bucket policy only disabled** (medium risk) — uniform bucket-level access wasn't enabled, meaning object-level ACLs could override intended permissions

Cross-checked both against the CIS Google Cloud Platform Foundation 2.0 compliance report, which flagged the same two rules as failing.

### 2. Remediated the issues
- Removed the `allUsers` principal from the Storage Object Viewer role, closing the public access hole
- Switched the bucket's access control from fine-grained to **uniform**, enforcing one consistent permission model across the bucket and its objects

### 3. Verified the fix
Re-ran the CIS compliance report and confirmed both findings dropped to 0 active issues.

## Key takeaways
- A single overlooked `allUsers` ACL entry is one of the most common (and most dangerous) cloud misconfigurations — it silently exposes data to the entire internet
- Uniform bucket-level access removes the risk of ACLs and IAM policies conflicting or being managed inconsistently
- Compliance reports aren't just for checkbox audits — they're a fast way to verify a remediation actually worked

## Tools
Google Cloud Security Command Center, Cloud Storage, CIS Google Cloud Platform Foundation 2.0 benchmark

---
*Completed as a Google Cloud Skills Boost lab.*
