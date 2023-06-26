# Azure live Honeynet with Live Traffic and Sentinel (SIEM) Geolocation

![Azure](https://github.com/HPastoral/Azure-SOC/assets/135756003/b5febe6b-38c9-430c-ab1c-318502cb14c7)

## Introduction

In this undertaking, I have constructed a compact honeynet within the Azure platform and established a mechanism to gather log data from diverse sources, channeling them into a Log Analytics workspace. This workspace is subsequently employed by Microsoft Sentinel to construct comprehensive attack maps, initiate alert notifications, and generate incident reports. To evaluate the security of the vulnerable environment, I conducted a 24-hour assessment of key security metrics. Following this, I implemented several security controls to fortify the environment and proceeded to measure the metrics for an additional 24 hours. The ensuing section presents the outcomes, showcasing the following metrics:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![NSGH MAP1](https://github.com/HPastoral/Azure-SOC/assets/135756003/3030a7dd-d482-4651-99cd-0b891214ee1c)<br>
![Linux MAP1](https://github.com/HPastoral/Azure-SOC/assets/135756003/8f25d594-7502-4766-b082-25106e2f35f3)
![MSSQL MAP1](https://github.com/HPastoral/Azure-SOC/assets/135756003/17924a2a-d6cb-419a-9771-d359814b8ee8)
![NSGH MAP1](https://github.com/HPastoral/Azure-SOC/assets/135756003/cae070d0-1118-4c03-8ce2-5f8079bd684b)

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-06-17 16:10:23
Stop Time 2023-06-17 16:11:08

| Metric                             | Count
| ---------------------------------- | -----
| SecurityEvent                      | 4750
| Syslog                             | 5113
| SecurityAlert                      | 0
| SecurityIncident                   | 355
| NSG Inbound Malicious Flows Allowed| 1653
| NSG Inbound Malicious Flows Blocked| 387
## Attack Maps After Hardening / Security Controls
```Some of the map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

![Linux MAP2](https://github.com/HPastoral/Azure-SOC/assets/135756003/7ff45c71-f69d-40fd-890e-9966653d42a5)<BR>

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-06-19 20:33:22
Stop Time	2023-06-19 20:34:00

| Metric                             | Count
| ---------------------------------- | -----
| SecurityEvent                      | 691
| Syslog                             | 25
| SecurityAlert                      | 0
| SecurityIncident                   | 0
| NSG Inbound Malicious Flows Allowed| 0
| NSG Inbound Malicious Flows Blocked| 0

## Conclusion

This project involved the construction of a compact honeynet within the Microsoft Azure platform, with the integration of log sources into a Log Analytics workspace. Microsoft Sentinel was utilized to activate alerts and generate incidents by leveraging the ingested logs. Furthermore, security metrics were initially measured in the vulnerable environment before implementing security controls, and then re-evaluated after the implementation. Notably, the application of security measures resulted in a significant reduction in the number of security events and incidents, effectively showcasing their efficacy.

