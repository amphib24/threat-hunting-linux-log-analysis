# Linux Log Analysis - Detecting SSH Attacks

## Scenario

&nbsp;&nbsp;&nbsp;  I am working as a SOC Level 1 Analyst for an MSSP. An IT administrator enabled public access to the ssh server, allowed password-based authentication, and used a weak password for the root account. It has been reported that the server may have suffered a brute-force credential attack, and I am tasked with investigating authentication logs to determine the impact and scope of the event.

## Potential Indicators of Attack (IOAs)

  -	A high volume of failed login attempts on repeated usernames, followed by a successful authentication.

## Analysis

### Sequential Login Attempts

#### Filter Used:

-	`cat /var/log/auth.log | grep sshd | grep -E “Accepted|Failed”`

#### Analyst Observation 1:

-	Initial investigation identified four accounts (root, sol, roy, user) involved in activity consistent with brute-force attacks conducted via SSH login attempts. The behavior is indicative of an automated attack originating from randomized IP addresses. The activity started on `2025-08-21 at 16:34:04.` 

<img width="1467" height="783" alt="initial discovery" src="https://github.com/user-attachments/assets/3bf423e5-06ee-4148-b09a-c1e419aa0a3f" />

#### Analyst Observation 2:

-	Further investigation identified a successful login to the root account at `17:10:08` from IP address `91[.]224[.]92[.]79`. Compromise of a root account can have severe consequences due to the account possessing the highest level of system privileges.

<img width="1851" height="462" alt="succesful_root_logon" src="https://github.com/user-attachments/assets/de32bacb-10e1-4c04-9b41-984a6e354a06" />

### Investigation of Further Actions

#### Filters Used:

1)	`cat /var/log/auth.log | grep ‘root’ | grep -E ‘useradd|passwd|usermod|userdel’`

2)	`cat /var/log/auth.log | grep -E ‘COMMAND=’`

3)	`cat /var/log/auth.log | grep -E ‘session opened|session closed’`

#### Analyst Observation:

-	Further investigation did not identify any additional suspicious activity following the compromise of the root account. 

## Conclusion

&nbsp;&nbsp;&nbsp; The investigation indicates behavior consistent with a brute-force attack via SSH login. The root account credentials were compromised, however, no further malicious activity was identified following the breach. It is recommended that account credentials be reset and password-based authentication be disabled and replaced with key-base authentication.
