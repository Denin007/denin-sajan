# Zabbix SIEM Homelab — SSH Brute Force Detection

## Overview
Built a working SIEM lab on Ubuntu 26.04 LTS (ARM64) running in UTM on Apple Silicon. Used Zabbix 7.4.11 to detect a simulated SSH brute force attack in real time, fired a High-severity alert, and produced a full SOC-style incident investigation report.

## Stack
| Component | Version |
|---|---|
| Zabbix Server | 7.4.11 |
| MySQL | 8.4.10 |
| Ubuntu Server | 26.04 LTS ARM64 |
| Zabbix Agent | 7.4.11 |
| Hydra (attacker) | v9.6 |
| Kali Linux | 2024.x |

## What I Built
1. Deployed Zabbix SIEM from scratch including MySQL backend
2. Configured Zabbix agent with a custom UserParameter to monitor SSH auth logs
3. Built a trigger using find() expression to detect Failed password patterns
4. Simulated SSH brute force from Kali using Hydra and 1,000 RockYou entries
5. Captured High-severity alert in Zabbix dashboard fired at 04:03:09 UTC
6. Wrote a full SOC-style incident investigation report

## MITRE ATT&CK Mapping
- T1110.001 - Brute Force: Password Guessing

## Key Detection Logic
UserParameter: sudo /usr/bin/tail -n 100 /var/log/auth.log
Trigger: find(/Zabbix server/ssh.auth.log,,"like","Failed password")=1

## Alert Fired
![Zabbix Alert](screenshots/zabbix%20problem%20page.png)

## Incident Report
- SSH_BruteForce_Incident_Report.docx
- SSH_BruteForce_Incident_Report_DeninSajan.docx.pdf

## Wordlist Attribution
1,000-entry subset of the RockYou 2009 breach dataset, distributed via
SecLists by Daniel Miessler: https://github.com/danielmiessler/SecLists
Pre-installed on Kali Linux. Used strictly for educational security research
in an isolated lab environment.

## Skills Demonstrated
- SIEM deployment and configuration
- Log monitoring and analysis
- Custom Zabbix UserParameter scripting
- Trigger expression writing
- SSH brute force simulation in controlled lab
- SOC-style incident documentation
- MITRE ATT&CK framework mapping

## Author
Denin Sajan - MSc Cyber Security, University of Hertfordshire
LinkedIn: https://linkedin.com/in/denin-sajan
GitHub: https://github.com/Denin007/denin-sajan
