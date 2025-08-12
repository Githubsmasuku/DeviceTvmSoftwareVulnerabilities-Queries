# DeviceTvmSoftwareVulnerabilities-Queries

## Overview
This repository contains Kusto Query Language (KQL) queries for analyzing software vulnerabilities in Microsoft Defender for Endpoint (MDE). It is designed to support cybersecurity professionals in identifying and managing device vulnerabilities, with a focus on streamlining remediation efforts in high-threat environments like South Africa’s financial and telecom sectors. The initial query targets devices affected by a specific Common Vulnerabilities and Exposures (CVE) identifier, enabling rapid identification of at-risk systems for patch management and compliance.

**Purpose:** To provide reusable, well-documented KQL queries for vulnerability management, showcasing expertise in MDE, cloud security, and compliance with South African regulations like the Protection of Personal Information Act (POPIA).

**Author:** [Your Name], a South African cybersecurity professional with 9 years of experience and certifications including CompTIA Security+, CISSP, and Microsoft AZ-500. Connect via [LinkedIn Profile].

## Repository Structure
```
DeviceTvmSoftwareVulnerabilities-Queries/
├── README.md                         # Repository overview and instructions
├── queries/                          # KQL query files
│   └── device-vulnerabilities-cve.kql  # Query for a specific CVE
├── docs/                             # Detailed documentation
├── results/                          # Sample (anonymized) query outputs
├── scripts/                          # Future automation scripts (e.g., Python, PowerShell)
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
| PC-001     | 12345    | Windows 10/11      | All          | All         |
| Server-007 | 67890    | Windows Server All | All          | All         |

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

## Getting Started
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/DeviceTvmSoftwareVulnerabilities-Queries.git
   ```
2. **Navigate to Query:** Open `queries/device-vulnerabilities-cve.kql` in a text editor.
3. **Customize:** Replace `<CVE-ID>` with the desired CVE identifier.
4. **Run in MDE:** Copy-paste into AHQ and execute.
5. **Contribute:** Add new queries or scripts via pull requests.

## Future Enhancements
- **Automation:** Develop Python or PowerShell scripts in `scripts/` to automate query execution via MDE APIs, streamlining recurring vulnerability checks.
- **Additional Queries:** Expand to include queries for other CVEs, unpatched systems, or end-of-life software.
- **Visualization:** Integrate with Power BI or Azure Dashboards for graphical vulnerability trends.
- **Compliance:** Map outputs to South African regulations (e.g., POPIA, Cybercrimes Act) to support audit requirements for organizations like the State Security Agency.

## Target Audience
- **SOC Analysts:** For daily vulnerability monitoring in high-demand sectors like finance and telecom.
- **Incident Responders:** To prioritize remediation of critical CVEs.
- **Compliance Teams:** To ensure alignment with South Africa’s regulatory frameworks.
- **Hiring Managers:** Demonstrates proficiency in KQL, MDE, and vulnerability management, relevant for roles in Johannesburg, Cape Town, or remote positions with international firms.

## Notes
- **Data Sensitivity:** Anonymize results in `results/` to comply with organizational policies and POPIA.
- **South Africa Context:** Designed for accessibility despite loadshedding; use offline tools (e.g., VS Code) and GitHub’s web interface for updates.
- **Feedback:** Submit suggestions via GitHub Issues or contact [Your Name] on LinkedIn.

## Acknowledgments
Built with insights from South Africa’s cybersecurity community, including ISACA SA and Absa Cybersecurity Academy, to address local challenges like skills shortages and compliance with the Cybercrimes Act.
