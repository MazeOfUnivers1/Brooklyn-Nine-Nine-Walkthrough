# Linux Enumeration Cheat Sheet

## Overview

Post-exploitation Linux enumeration focuses on identifying misconfigurations, credentials, and privilege escalation vectors after gaining an initial foothold on a system.

## Common Syntax

Manual enumeration commands, or automated scripts such as `linpeas.sh`.

## Useful Commands

```bash
# Current user and privileges
whoami
id
sudo -l

# System and kernel information
uname -a
cat /etc/os-release

# Running processes
ps aux

# Network information
ip a
netstat -tulpn

# Scheduled tasks
crontab -l
cat /etc/crontab

# SUID/SGID binaries
find / -perm -4000 -type f 2>/dev/null
find / -perm -2000 -type f 2>/dev/null

# World-writable files
find / -writable -type f 2>/dev/null

# Automated enumeration
./linpeas.sh
```

## Important Options

| Command | Description |
|---|---|
| `sudo -l` | Lists commands the current user may run via `sudo` |
| `id` | Displays current user, group, and group memberships |
| `find / -perm -4000` | Finds SUID binaries, which run with the file owner's privileges |
| `crontab -l` | Lists scheduled cron jobs for the current user |
| `linpeas.sh` | Community-maintained automated Linux privilege escalation enumeration script |

## Examples

```text
jake@brookly_nine_nine:/tmp$ sudo -l
User jake may run the following commands on brookly_nine_nine:
    (ALL) NOPASSWD: /usr/bin/less
```

Sudo enumeration directly revealed a privilege escalation path (see [07-Privilege-Escalation](../docs/07-Privilege-Escalation/README.md)).

## Common Mistakes

- Skipping `sudo -l` as one of the very first post-foothold checks.
- Not cross-referencing discovered SUID binaries or sudo-permitted commands against GTFOBins.
- Running automated tools (like `linpeas.sh`) without also understanding what they check for manually.

## References

- [GTFOBins](https://gtfobins.org/)
- [LinPEAS (PEASS-ng)](https://github.com/peass-ng/PEASS-ng)

## Key Takeaways

- `sudo -l` and SUID binary discovery are two of the highest-value, lowest-effort enumeration steps after gaining a foothold.
- Automated tools accelerate enumeration but should be paired with an understanding of what they're checking for.
