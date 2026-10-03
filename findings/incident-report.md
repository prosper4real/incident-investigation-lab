# Incident Investigation Report

## Incident Type

Suspected SSH credential compromise followed by privileged activity.

## Investigation Scope

This investigation analyzes a synthetic SSH authentication log created for a controlled cybersecurity training lab.

## Key Indicators

| Indicator | Evidence |
|---|---|
| Source IP | `185.220.101.42` |
| Target account | `analyst` |
| Failed attempts | 7 |
| Successful authentication | 08:42:03 |
| Privileged activity | Yes |
| Session | Opened at 08:42:17 and closed at 08:44:07 |

## Timeline

### 08:41:12 – 08:41:41

Five failed SSH authentication attempts targeted the invalid `admin` account from `185.220.101.42`.

### 08:42:03

Authentication succeeded for the `analyst` account from the same source IP.

### 08:42:17

An SSH session was opened for `analyst`.

### 08:43:02

The account executed `/usr/bin/id` using `sudo` with root privileges.

### 08:43:19

The account executed `/usr/bin/cat /etc/passwd` using `sudo` with root privileges.

### 08:44:07

The SSH session for `analyst` was closed.

### 08:45:12 – 08:45:19

Two additional failed authentication attempts targeted the invalid `test` account from the same source IP.

## Analysis

The log shows repeated failed SSH authentication attempts from a single source IP, followed by successful authentication to the `analyst` account from that same IP.

After authentication, the account opened an SSH session and used `sudo` to execute commands with root privileges. The commands included system identity discovery and reading `/etc/passwd`.

The sequence is consistent with a simulated account-compromise scenario followed by privileged reconnaissance.

Because this is a synthetic training dataset, the log alone does not establish that a real-world compromise occurred.

## Indicators of Compromise

- Source IP: `185.220.101.42`
- Target account: `analyst`
- Repeated failed SSH authentication
- Successful SSH authentication after failed attempts
- `sudo` activity
- Access to `/etc/passwd`

## Recommended Defensive Actions

1. Investigate the `analyst` account and verify whether the successful login was authorized.
2. Review authentication logs from the same source IP for additional activity.
3. Rotate credentials if unauthorized access is confirmed.
4. Review and restrict unnecessary `sudo` privileges.
5. Consider SSH hardening measures such as key-based authentication and disabling password authentication where appropriate.
6. Monitor repeated authentication failures and successful logins from the same source.

## Evidence

Primary evidence:

- `logs/auth.log`

Analysis commands were performed using standard Linux command-line tools including `grep`, `awk`, `sort`, and `uniq`.

## Disclaimer

This investigation uses a synthetic log dataset created specifically for cybersecurity education and portfolio demonstration. No real system or unauthorized account was investigated.
