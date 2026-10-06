# Incident Investigation & Log Analysis Lab

## Overview

This project demonstrates a structured approach to investigating a simulated SSH-based security incident using authentication logs. The goal was to identify suspicious activity, reconstruct a clear incident timeline, extract indicators of compromise (IOCs), and provide actionable defensive recommendations.

## Lab Environment

| Component              | Details                                      |
|------------------------|----------------------------------------------|
| Platform               | Kali Linux                                   |
| Data Source            | Synthetic SSH authentication log             |
| Analysis Tools         | grep, awk, sort, uniq                        |
| Environment            | Controlled cybersecurity training lab        |

## Investigation Scenario

The log contains repeated failed authentication attempts followed by a successful login from the same source IP. After authentication, the account performed privileged actions using `sudo`, including system reconnaissance commands.

## Key Findings

- **7 failed authentication attempts**
- Source IP: `185.220.101.42`
- Successful authentication to the `analyst` account
- SSH session opened after successful login
- Privileged `sudo` activity executed
- Access to `/etc/passwd`
- Additional failed authentication attempts after the session ended

## Incident Timeline

| Time                  | Activity                                              |
|-----------------------|-------------------------------------------------------|
| 08:41:12 – 08:41:41   | Five failed attempts against invalid user `admin`     |
| 08:42:03              | Successful login as `analyst`                         |
| 08:42:17              | SSH session opened for `analyst`                      |
| 08:43:02              | `sudo id` executed with root privileges               |
| 08:43:19              | `sudo cat /etc/passwd` executed                       |
| 08:44:07              | SSH session closed                                    |
| 08:45:12 – 08:45:19   | Two additional failed attempts against user `test`    |

## Indicators of Compromise (IOCs)

- **Source IP:** 185.220.101.42
- **Compromised Account:** analyst
- Repeated failed SSH authentication attempts
- Successful authentication following multiple failures
- Privileged sudo activity after login
- Access to sensitive system file (`/etc/passwd`)

## Analysis Summary

The activity pattern is consistent with a credential-based attack:

1. Brute-force / password spraying attempts against common usernames
2. Successful authentication to a valid account
3. Immediate privileged reconnaissance using `sudo`
4. Continued authentication attempts after the session ended

Because this is a synthetic training dataset, the log alone does not confirm a real-world compromise. However, the sequence provides a realistic example of how an attacker may behave after gaining initial access.

## Defensive Recommendations

1. Verify whether the successful `analyst` login was authorized
2. Review all authentication activity originating from `185.220.101.42`
3. Rotate credentials if unauthorized access is confirmed
4. Restrict unnecessary `sudo` privileges
5. Enforce SSH key-based authentication and disable password authentication where possible
6. Implement monitoring and alerting for repeated authentication failures and unusual successful logins
7. Consider geo-blocking or rate-limiting for SSH where appropriate

## Evidence

- **Primary Log:** `logs/auth.log`
- **Investigation Report:** `findings/incident-report.md`

## Skills Demonstrated

- Linux log analysis
- Authentication event investigation
- Incident timeline reconstruction
- Indicator of Compromise (IOC) identification
- Basic threat analysis
- Clear security documentation
- Command-line investigation techniques

## Disclaimer

This project uses a synthetic log dataset created specifically for cybersecurity education and portfolio demonstration. No real systems or unauthorized accounts were investigated.
