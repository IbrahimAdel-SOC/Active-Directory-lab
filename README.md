# Active Directory Lab

## Objective

The Active Directory Lab project aimed to build a controlled environment for simulating and detecting real-world cyber attacks. The lab consists of a Splunk SIEM server, a Windows Server running Active Directory, a Windows 10 victim machine, and a Kali Linux attacker machine — all connected on the same internal network `192.168.10.0/24` under the domain **Ibrahim**. The primary focus was to forward and analyze logs within Splunk, using Kali Linux to launch attacks and Sysmon to generate detailed endpoint telemetry, simulating a real SOC analyst workflow.

---

### Skills Learned

- Deploying and configuring Splunk as a SIEM for centralized log ingestion and analysis.
- Setting up Active Directory and joining Windows endpoints to a domain.
- Installing and tuning Sysmon for enhanced Windows event telemetry (process creation, network connections, file events).
- Configuring Splunk Universal Forwarder to ship logs from Windows machines to the Splunk indexer.
- Performing offensive operations from Kali Linux including reconnaissance, brute force, and exploitation.
- Writing SPL (Search Processing Language) queries to detect and investigate malicious activity.
- Mapping attack techniques to the MITRE ATT&CK framework.
- Identifying Indicators of Compromise (IOCs) from Windows Event Logs and Sysmon data.
- Developing end-to-end understanding of the attack lifecycle from the attacker and defender perspective.

---

### Tools Used

| Tool | Purpose |
|---|---|
| Splunk Enterprise | SIEM — log ingestion, search, alerting, and dashboards |
| Splunk Universal Forwarder | Forwards Windows logs to Splunk indexer on port 9997 |
| Sysmon | Enhanced Windows telemetry — process, network, and file events |
| Active Directory | Domain controller — user and machine management |
| Kali Linux | Attacker machine — offensive tools and manual exploitation |
| Windows 10 | Victim endpoint joined to the domain |
| VirtualBox | Hypervisor running all lab VMs |

---

## Steps

**Ref 1 — Network Diagram**

Overview of the lab topology showing all four machines, their assigned IPs, and the log forwarding flow from Windows endpoints to Splunk SIEM through the internal switch.

<img width="711" height="629" alt="Active Directory Diagram drawio" src="https://github.com/user-attachments/assets/681d3189-68c3-4e08-9998-9b9107dc61b8" />

---
**Ref 2 — Virtual Machines Setup**

All four VMs configured inside Oracle VirtualBox: ADDC (Active Directory Domain Controller), Splunk Server, Windows 10 victim machine, and Kali Linux attacker machine — all powered off and ready to be launched for the lab.

<img width="1442" height="783" alt="image" src="https://github.com/user-attachments/assets/51644a1e-5c4f-4a8a-ae06-e51a5a893d70" />

---

**Ref 2b — Splunk Server Network Configuration**
Static IP address configured on the Splunk Server using netplan (/etc/netplan/50-cloud-init.yaml), assigning 192.168.10.10/24 with gateway 192.168.10.1 and DNS 8.8.8.8.

<img width="961" height="353" alt="image" src="https://github.com/user-attachments/assets/546e6bd8-2d16-44b9-923a-10e89317895c" />

---

