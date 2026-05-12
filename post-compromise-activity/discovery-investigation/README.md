# Linux Log Analysis - SIEM Alert Investigation (Supicious Discovery Command)

## Scenario

&nbsp;&nbsp;&nbsp; I am working as a SOC Level 1 Analyst for an MSSP. A SIEM alert was triggered for suspicious Linux discovery command execution (hostname) via the itsupport user account. I have been tasked with investigating the alert, tracing the executed command, analyzing related process activity, and building a process tree to determine the scope and impact of the event.

## Analysis

### Search For Parent Process ID (PPID)

#### Filter used: 

-	ausearch -i -x hostname

#### Analyst Observation:

-	Investigation into the hostname command execution identified a PPID of 3771, indicating the command was executed by another process. Further analysis of the parent process is required to determine the process name and determine the nature of the activity.

<img width="1858" height="200" alt="hostname_pid_and_ppid" src="https://github.com/user-attachments/assets/99a0a9b2-8dac-429f-9301-a1706513cbe7" />

### Identify Parent Process

#### Filter Used:

-	ausearch -i --pid 3771

#### Analyst Observation:

-	Investigation into the parent process identified a script named debug.sh executed from the /home/itsupport directory. This behavior is suspicious, as scripts executed from user directories may indicate unauthorized activity. Further investigation is needed to determine whether the activity was legitimate or malicious.  

<img width="1852" height="146" alt="debug sh" src="https://github.com/user-attachments/assets/8e640bbe-4cc7-4e79-a341-90dda91f2b3f" />


### Investigate Activity Related to debug.sh

#### Filter Used:

-	ausearch -i --ppid 3371

#### Analyst Observation:

-	Multiple child processes were identified as originating from debug.sh. The behavior suggests the script is gathering system monitoring and troubleshooting information such as CPU and memory usage. No indicators of malicious activity were identified in the process execution chain. Further review of the script contents needs to be performed to confirm its intended functionality.

<img width="1846" height="397" alt="hostname command" src="https://github.com/user-attachments/assets/939a48ec-e90d-4993-92de-aba25fcb2a51" />

<img width="1843" height="392" alt="ps commands" src="https://github.com/user-attachments/assets/76fa3bf2-cf38-4e2c-a6a5-c269861aa754" />

### Investigate Script Contents

#### Filter Used: 

-	cat /home/itsupport/debug.sh

#### Analyst Observation:

-	Review of the script contents confirms the script is used by the IT support team to collect system load data for debugging purposes. The script includes a contact email (greg@tryhackme[.]thm) for reporting any security concerns, which further validates its legitimacy. 

<img width="817" height="518" alt="script contents" src="https://github.com/user-attachments/assets/58a656fd-79e1-412d-a685-53e13cb02482" />

## Conclusion

&nbsp;&nbsp;&nbsp Investigation into the process tree associated with the discovery command (hostname) indicates the activity originated from a legitimate script used by the IT support team. Based on the evidence reviewed, the alert is assessed as a false positive, and the incident can be closed with no further action required.

## Process Tree

 ```text
itsupport
|__ debug.sh
    |-- hostname
       |--uname -a
       |-- lscpu
       |-- free -h
       |-- df -hT
       |__ ps 

```
