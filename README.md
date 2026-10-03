# Incident Investigation & Log Analysis Lab

## Objective

Investigate a simulated SSH security incident using authentication logs, identify suspicious activity, reconstruct the incident timeline, and document indicators of compromise and defensive actions.

## Lab Environment

- Platform: Kali Linux
- Data source: Synthetic SSH authentication log
- Analysis tools: `grep`, `awk`, `sort`, `uniq`
- Environment: Controlled cybersecurity training lab

## Investigation Scenario

The investigation focuses on authentication activity involving an SSH service.

The log contains repeated failed authentication attempts followed by a successful login from the same source IP. The authenticated account subsequently performed privileged actions using `sudo`.

## Investigation Findings

The investigation identified:

- 7 failed authentication attempts
- Source IP: `185.220.101.42`
- Successful authentication to the `analyst` account
- SSH session opened after successful authentication
- Privileged `sudo` activity
- Access to `/etc/passwd`
- Additional failed authentication attempts after the session ended

## Incident Timeline

| Time | Activity |
|---|---|
| 08:41:12–08:41:41 | Five failed attempts against `admin` |
| 08:42:03 | Successful login as `analyst` |
| 08:42:17 | SSH session opened |
| 08:43:02 | `sudo id` executed |
| 08:43:19 | `/etc/passwd` accessed with `sudo` |
| 08:44:07 | SSH session closed |
| 08:45:12–08:45:19 | Two additional failed attempts against `test` |

## Indicators of Compromise

- IP address: `185.220.101.42`
- Account: `analyst`
- Repeated failed SSH authentication
- Successful authentication following failed attempts
- Privileged `sudo` activity
- Access to `/etc/passwd`

## Defensive Recommendations

- Verify whether the `analyst` login was authorized.
- Review additional authentication activity from the source IP.
- Rotate credentials if unauthorized access is confirmed.
- Review and restrict unnecessary `sudo` privileges.
- Consider SSH key-based authentication.
- Monitor repeated authentication failures and unusual successful logins.

## Evidence

Primary log:

- `logs/auth.log`

Investigation report:

- `findings/incident-report.md`

## Skills Demonstrated

- Linux log analysis
- Authentication event analysis
- Incident timeline reconstruction
- Indicator identification
- Basic threat investigation
- Security documentation
- Command-line investigation

## Disclaimer

This project uses a synthetic log dataset created for cybersecurity education and portfolio demonstration. No real system or unauthorized account was investigated.
