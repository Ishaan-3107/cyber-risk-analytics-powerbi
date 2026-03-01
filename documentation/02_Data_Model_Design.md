# Data Model Design

## Overview

This project contains two primary analytical datasets:

- Exceptions Data
- Vulnerability Data

Both datasets are structured to support KPI reporting, trend analysis, and risk-based segmentation within Power BI.

---

# Exceptions Data Model

## Table: Exceptions

Each row represents a single exception record.

### Columns

- S. No.
- Request_Type
- Exception_required_for
- Exception_Other
- Created
- Created_by
- Department
- Department_Head
- Domain Expert
- Phone
- Risk_Rating
- Status
- Duration_for_exception
- Exception_DurationUpTo
- Extension_Required_Date
- ExtensionUpTo
- ExtensionStatus
- Is_Extension
- HOD_Approval
- Ext.History
- Unique_ID

### Measures

- Total Exceptions
- Exceptions Approved
- Exceptions Rejected
- Approval Rate
- Rejection Rate

### Date Fields Used

- Created
- Exception_DurationUpTo
- Extension_Required_Date
- ExtensionUpTo

These fields are used for lifecycle tracking and time-based analysis.

---

# Vulnerability Data Model

## Table: Vulnerability Data

Each row represents a vulnerability instance associated with a host and port.

### Columns

- S. No.
- Asset Identifier
- Asset Criticality
- Hostname
- Host IP
- Host Rank
- Host Count
- Port
- Port Vuln Count
- Severity
- Critical Vulns
- High Vulns
- Total Vulns
- Critical %
- Top Host
- Top Port
- Month
- Month Number
- Month Year
- Year

### Measures

- Total Vulns
- Critical Vulns
- High Vulns
- Critical %
- Host Count
- Port Vuln Count
- Top Host
- Top Port

### Time Fields Used

- Month
- Month Number
- Month Year
- Year

These fields support monthly aggregation and severity trend analysis.

---

## Modeling Notes

- Separate logical datasets for Exceptions and Vulnerabilities
- Measures created for KPI reporting
- Date-based aggregation using month and year fields
- Simple and maintainable structure focused on analytical reporting
