# Linux Threat Hunting and Log Analysis
&nbsp;&nbsp;&nbsp; This repository is a collection of SOC-level threat detection investigations utilizing Linux log analysis. The investigations follow the labs from TryHackMe's SOC 1 Linux Threat Detection rooms, and are structured to simulate real-world SOC workflows. The investigations are broken into three main categories: initial access, post-compromise activities, and persistence mechanisms. The purpose of this repository is to demonstrate a SOC analyst's approach to investigating threat activity on Linux hosts using native logging tools.

# Repository Status
  Work in progress - continually updated as I complete write-ups
## Demonstrated Skills

 - Linux authentication log analysis (/var/log/auth.log)
 - Log filtering and correlation using command-line tools
 - Extraction and documentation of indicators of compromise (IOCs) from system logs
 - Privilege escalation analysis via sudo and account management activity
 - Post-compromise activity scoping and behavioral analysis
 - User account activity monitoring (creation, modification, deletion)

### Initial Access

&nbsp;&nbsp;&nbsp; This section contains investigations into initial access activity on Linux hosts and servers. There are various techniques an attacker can leverage to gain initial access. These investigations focus on SSH brute force and other service-based initial access vectors.

#### Technical Write-Ups

<a href="https://github.com/amphib24/threat-hunting-linux-log-analysis/tree/main/initial-access-investigations/detecting-ssh-attacks">SSH Brute Force</a>

### Post Compromise

&nbsp;&nbsp;&nbsp; This section contains investigations into initial access activity on Linux hosts and servers. These investigations focus on analyzing a suspected malicious discovery command and cryptominer activity.

#### Technical Write-Ups

<a href = "https://github.com/amphib24/threat-hunting-linux-log-analysis/tree/main/post-compromise-activity/discovery-investigation">Discovery Command</a>
