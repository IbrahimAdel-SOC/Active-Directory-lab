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
| Nmap | Network scanning and service discovery |
| Hydra | Brute-force attacks against RDP and SMB services |
| Metasploit Framework | Exploitation and post-exploitation from Kali |
| VirtualBox | Hypervisor running all lab VMs |

---

## Steps

**Ref 1 — Network Diagram**

Overview of the lab topology showing all four machines, their assigned IPs, and the log forwarding flow from Windows endpoints to Splunk SIEM through the internal switch.

<img width="711" height="629" alt="Active Directory Diagram drawio" src="https://github.com/user-attachments/assets/681d3189-68c3-4e08-9998-9b9107dc61b8" />

---

**Ref 2 — Virtual Machines Setup**

All four VMs running inside VirtualBox: Splunk Server (192.168.10.10), Active Directory / Windows Server (192.168.10.7), Windows 10 victim (DHCP), and Kali Linux attacker (192.168.10.250).

*drag & drop screenshot here*

---

**Ref 3 — Active Directory Configuration**

Windows Server promoted to Domain Controller under the domain **Ibrahim**. Windows 10 machine successfully joined to the domain and appears in AD Users and Computers.

*drag & drop screenshot here*

---

**Ref 4 — Sysmon Installation**

Sysmon installed on both Windows Server and Windows 10 using a custom configuration file. Sysmon service confirmed running on both machines, capturing detailed event telemetry.

*drag & drop screenshot here*

---

**Ref 5 — Splunk Universal Forwarder Configuration**

Splunk Universal Forwarder installed on both Windows machines. Configured `inputs.conf` to collect Security, System, and Sysmon (`Microsoft-Windows-Sysmon/Operational`) event logs and forward them to Splunk on port 9997.

*drag & drop screenshot here*

---

**Ref 6 — Splunk Receiving Logs**

Splunk web interface showing live events being received from both Windows endpoints in the `endpoint` index. Both hostnames visible as data sources confirming successful log forwarding.

*drag & drop screenshot here*

---

**Ref 7 — Reconnaissance from Kali (Nmap)**

Nmap scan launched from Kali Linux (192.168.10.250) against the internal network `192.168.10.0/24` to enumerate live hosts and discover open ports and running services.

*drag & drop screenshot here*

---

**Ref 8 — Brute Force Attack from Kali (Hydra)**

Hydra used from Kali to brute-force RDP or SMB credentials against the Windows 10 victim machine. Multiple failed authentication attempts generated against the target.

*drag & drop screenshot here*

---

**Ref 9 — Detection in Splunk — Brute Force (Event ID 4625)**

Splunk SPL query detecting a high volume of failed logon attempts (Windows Event ID 4625) originating from the attacker IP (192.168.10.250) within a short time window — a clear indicator of a brute-force attack.

*drag & drop screenshot here*

---

**Ref 10 — Detection in Splunk — Sysmon Network & Process Events**

Sysmon Event ID 3 (network connection) and Event ID 1 (process creation) captured in Splunk, showing suspicious outbound connections and processes spawned on the victim machine following the attack from Kali.

*drag & drop screenshot here*
