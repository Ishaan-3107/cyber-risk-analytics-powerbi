# DAX Measures

## Core Measures

Total Exceptions = COUNTROWS(Sheet1)

Exceptions Approved = CALCULATE(COUNTROWS(Sheet1), Sheet1[Status] = "Approve")

Exceptions Rejected = CALCULATE(COUNTROWS(Sheet1), Sheet1[Status] IN {"Rejected by Domain Expert", "Rejected by HOD", "Rejected by Security Head"})

Approval Rate = DIVIDE([Exceptions Approved], DISTINCTCOUNT(Sheet1[Unique_ID]))

Rejection Rate = DIVIDE([Exceptions Rejected], DISTINCTCOUNT(Sheet1[Unique_ID]))

Total Vulnerabilities = COUNTROWS('Vulnerability Data')

Critical Vulnerabilities = CALCULATE([Total Vulnerabilities], 'Vulnerability Data'[Severity] = "Critical")

High Vulnerabilities = CALCULATE([Total Vulnerabilities], 'Vulnerability Data'[Severity] = "High")

Critical % = DIVIDE([Critical Vulnerabilities], [Total Vulnerabilities])

Host Count = COUNTROWS('Vulnerability Data')

Host Rank = RANKX(ALLSELECTED('Vulnerability Data'[Hostname]), [Total Vulnerabilities],
, DESC, Dense)

Top Host = 
VAR HostTable = SUMMARIZE('Vulnerability Data', 'Vulnerability Data'[Hostname], "HostValue", [Host Count])
VAR CleanTable = FILTER(HostTable, 'Vulnerability Data'[Hostname] <> "-" && NOT ISBLANK('Vulnerability Data'[Hostname]))
VAR TopHost = TOPN(1, CleanTable, [HostValue], DESC, 'Vulnerability Data'[Hostname], ASC)
RETURN MAXX(TopHost, 'Vulnerability Data'[Hostname])

Port Vulnerability Count = COUNTROWS('Vulnerability Data')

Top Port = 
VAR PortTable = SUMMARIZE('Vulnerability Data', 'Vulnerability Data'[Port], "PortValue", [Port Vulnerability Count])
VAR TopPort = TOPN(1, PortTable, [PortValue], DESC, 'Vulnerability Data'[Port], ASC)
return MAXX(TopPort, 'Vulnerability Data'[Port])
