# DeviceTvmSoftwareVulnerabilities-Queries

## Overview
This repository contains Kusto Query Language (KQL) queries for analyzing software vulnerabilities in Microsoft Defender for Endpoint (MDE). It is designed to support cybersecurity professionals in identifying and managing device vulnerabilities, with a focus on streamlining remediation efforts in high-threat environments like South Africa’s financial and telecom sectors. The initial query targets devices affected by a specific Common Vulnerabilities and Exposures (CVE) identifier, enabling rapid identification of at-risk systems for patch management and compliance.

**Purpose:** To provide reusable, well-documented KQL queries for vulnerability management, showcasing expertise in MDE, cloud security, and compliance with South African regulations like the Protection of Personal Information Act (POPIA).

**Author:** Sihle Masuku, a South African cybersecurity professional with 9 years Technical experience with 4 years Cybersecurity experience. My [DeviceTvmSoftwareVulnerabilities.docx](https://github.com/user-attachments/files/21734606/DeviceTvmSoftwareVulnerabilities.docx)
certifications including CCNA (Switching and Routing),CompTIA Security+, SecurityX, and Microsoft AZ-500 in progress. Connect via [https://www.linkedin.com/in/sihle-masuku-securityx-411b0416b/].

## Repository Structure
```
DeviceTvmSoftwareVulnerabilities-Queries/
├── README.md                         # Repository overview and instructions
├── queries/                          # KQL query files
│   └── device-vulnerabilities-cve.kql  # Query for a specific CVE
├── docs/                             # Detailed documentation
├── results/                          # Sample (anonymized) query outputs
├── scripts/                          # Future automation scripts (Powershell and Python)
└── .gitignore                        # Excludes sensitive files
```

## Key Query: Device Vulnerabilities by CVE
- **File:** `queries/device-vulnerabilities-cve.kql`
- **Description:** Identifies devices vulnerable to a specific CVE in MDE’s `DeviceTvmSoftwareVulnerabilities` table, summarizing by device name, ID, operating system, and software details.
- **Query:**
  ```kql
  DeviceTvmSoftwareVulnerabilities| where CveId in ("<CVE-ID>")| summarize by DeviceName, DeviceId, strcat(OSPlatform, " ", OSVersion), SoftwareName, SoftwareVersion
  ```

### Purpose
- **Objective:** Pinpoint devices affected by a specific CVE to prioritize patching or mitigation, critical for organizations facing high-severity threats.
- **Use Case:** Supports Security Operations Center (SOC) analysts and incident responders in vulnerability management, ensuring compliance with South African regulations like POPIA and the Cybercrimes Act.
- **Relevance:** Addresses South Africa’s growing cyber threats, particularly in banking (e.g., Absa, Standard Bank) and telecom (e.g., MTN, Vodacom), where rapid vulnerability identification is essential due to a reported 22% increase in cyberattacks annually.

### Query Breakdown
1. **Data Source:** Queries MDE’s `DeviceTvmSoftwareVulnerabilities` table via the Advanced Hunting Query (AHQ) interface.
2. **Filter:** Uses `where CveId in ("<CVE-ID>")` to isolate records for a specified CVE, ensuring targeted results.
3. **Output:** Groups results by:
   - `DeviceName`: Hostname of the affected device.
   - `DeviceId`: Unique MDE identifier.
   - `strcat(OSPlatform, " ", OSVersion)`: Combined OS platform and version (e.g., “Windows 10 22H2”).
   - `SoftwareName`: Name of the vulnerable software.
   - `SoftwareVersion`: Affected software version.
4. **Outcome:** Produces a table for actionable remediation planning, such as prioritizing patches for critical systems.

### Expected Output
| DeviceName | DeviceId | OSPlatform_OSVersion | SoftwareName | SoftwareVersion |
|------------|----------|---------------------|--------------|-----------------|
| PC Name     | *    | Windows 10/11       | All           | All         |
| Server Name | *    | Windows Server All  | All           | All         |

*Note:* Results depend on the organization’s environment and the specified CVE. Export as CSV/JSON for reporting or SIEM integration.

### Usage Instructions
1. **Access MDE:** Log into the MDE portal (security.microsoft.com) and navigate to Advanced Hunting Query.
2. **Run Query:**
   - Copy the query from `queries/device-vulnerabilities-cve.kql`.
   - Replace `<CVE-ID>` with the target CVE identifier (e.g., “CVE-2023-12345”).
   - Paste into the AHQ editor and execute.
3. **Analyze Results:**
   - Identify critical devices (e.g., servers vs. workstations) for urgent patching.
   - Cross-reference with patch management tools to confirm available updates.
   - Escalate high-risk findings to the incident response team.
4. **Export:** Save results as CSV for stakeholder reports or JSON for integration with tools like Azure Sentinel.
5. **South Africa Context:** Save queries locally to mitigate loadshedding disruptions; use GitHub’s mobile app (iOS/Android) for updates during power outages.
