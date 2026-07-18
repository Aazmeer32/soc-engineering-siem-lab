# Cross-Platform SOC Engineering & Detection Lab

##  Project Overview
This project details the architecture, deployment, and optimization of an enterprise-grade Security Operations Center (SOC) home lab environment running within a completely isolated host-only network topology (`192.168.30.0/24`). 

The lab successfully integrates cross-platform telemetry ingestion (Windows Security Logs via Microsoft Sysmon & Linux `auth.log`) into a centralized Splunk SIEM instance. It demonstrates real-world threat simulation, network diagnostics, and detection engineering optimizations to resolve unparsed log pitfalls.

---

##  Tech Stack & Architecture
* **Virtualization Layer:** VirtualBox Engine (Isolated Host-Only Subnets)
* **SIEM Core:** Splunk Enterprise (Data ingestion on TCP port `9997`)
* **Defensive Baseline:** Windows 10 Target Hardened with Sysmon v15.21 (XML Config schema v4.91) & Ubuntu SSH Target
* **Attacker Suite:** Arch Linux equipped with Nmap and THC-Hydra

---

##  Lab Execution Phases

### Phase 1: Network Topology & Layer-2 Diagnostic Battle
* Configured virtual switch interfaces to maintain zero production leakage.
* Diagnosed and resolved a total communication freeze (100% packet loss) by flushing stale ARP neighbor tables (`sudo ip neigh flush all`) and deploying inbound PowerShell firewall rule adjustments for ICMP validation:
  ```powershell
  New-NetFirewallRule -DisplayName "Allow Lab Pings" -Direction Inbound -Action Allow -Protocol ICMPv4