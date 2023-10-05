# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I created a mini honeynet in Azure to observe adversarial behaviors by configuring vulnerable resources to attract malicious actors. Leveraging Azure Sentinel's SIEM capabilities, I ingested various log sources into a centralized Log Analytics workspace to gain visibility, including:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

By establishing threat detection rules, Sentinel was able to generate alerts and incidents based on suspicious activities observed within the honeynet. This provided hands-on experience with constructing controlled threat environments, ingesting and correlating security telemetry, and configuring detection and response mechanisms using a cloud-based SIEM

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The miniature honeynet environment within Azure was comprised of the following core components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the baseline "BEFORE" metrics, all honeynet resources were internet-facing with permissive network and host firewall policies, exposing public endpoints.

For the "AFTER" metrics, network access controls were tightened by restricting ingress to a single administrative source. Additional layers of protection were added through host firewall policies and use of private endpoints.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>

## Metrics Before Hardening / Security Controls

The table below presents key security metrics measured within the untreated honeynet environment over a 24-hour observation period:


Start Time 2023-09-20 11:08:04 PM
Stop Time 2023-09-21 11:08:04 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 24022
| Syslog                   | 1575
| SecurityAlert            | 10
| SecurityIncident         | 129
| AzureNetworkAnalytics_CL | 3214

## Attack Maps Before Hardening / Security Controls

```After hardening the environment, map queries for the 24 hour observation period returned no results, indicating the security controls implemented successfully prevented malicious activity within the honeynet.```

## Metrics After Hardening / Security Controls

The following table displays key security metrics measured within the hardened honeynet environment over a subsequent 24-hour observation window, following implementation of security controls:

Start Time 2023-09-23 10:01:07 AM
Stop Time 2023-09-24 10:15:04 AM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 4420
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In summary, this project demonstrated hands-on skills in designing honeynets, integrating security data sources, configuring detection rules, and measuring the impact of controls through metrics analysis. The experience gained with adversarial simulation, SIEM workflows, and quantifying security enhancements provides key competencies for cybersecurity roles.
