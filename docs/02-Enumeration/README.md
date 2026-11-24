# Enumeration

## Overview

Enumeration builds on the reconnaissance results. With three open ports identified (FTP, SSH, HTTP), this phase focuses on interpreting the Nmap output to prioritize which service to investigate first, and why.

## Objectives

- Interpret the detailed Nmap service/version output from the recon phase
- Prioritize services based on exposed attack surface
- Identify the most promising lead for gaining a foothold

## Important Terminology

| Term | Definition |
|---|---|
| Attack surface | The set of points where an attacker can attempt to interact with a system |
| Anonymous authentication | A service configuration that allows login without valid credentials |
| Banner grabbing | Identifying software and version information from a service's response |

## Concepts Explained

The Nmap scan from the recon phase (`-A -p- -T3`) returned version-specific banners for all three open services, along with NSE script output. Rather than attacking blindly, each service's banner and any script output is reviewed first to decide where to focus.

## Commands and Syntax

No new commands were run in this phase. This section documents analysis of the output already gathered during reconnaissance.

## Command Breakdown

Not applicable. See [01 – Recon](../01-Recon/README.md) for the originating scan command breakdown.

## Examples

Referencing the scan results from the recon phase:

```text
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0             119 May 17  2020 note_to_jake.txt
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
```

## Screenshots

No additional screenshots were captured for this phase. See [01 – Recon](../01-Recon/README.md#screenshots) for the source scan output.

## Observations

| Port | Service | Priority | Reasoning |
|---|---|---|---|
| 21 | FTP (vsftpd 3.0.3) | High | Anonymous login confirmed by `ftp-anon`, with a readable file already listed |
| 80 | HTTP (Apache 2.4.29) | Medium | Web server is up but the banner grab returned no page title, requiring manual review |
| 22 | SSH (OpenSSH 7.6p1) | Low, initially | No anonymous access; requires valid credentials, making it a target for later stages |

> [!TIP]
> When a service explicitly advertises anonymous or unauthenticated access, as `ftp-anon` did here, it is almost always worth investigating first. It often yields direct leads such as credentials, notes, or configuration files.

## Common Mistakes

- Attacking SSH directly with brute force before checking for easier, unauthenticated leads
- Ignoring NSE script output embedded in the `-A` scan results
- Not correlating findings across services, such as a note found on FTP referencing a username relevant to SSH

## Notes

- Based on this analysis, FTP was prioritized for the next phase due to confirmed anonymous access and a visible file.
- The HTTP service was also reviewed manually; see [03 – Web](../03-Web/README.md).

## Additional Context

> [!NOTE]
> The following is supplementary information, not derived from the lab notes.

A common enumeration priority order in CTF and lab environments is to check for anonymous FTP, SMB, or NFS access first, then review web applications, and attempt credentialed access to SSH or RDP last, since it typically depends on material gathered during earlier steps.

## References

- [Nmap Scripting Engine (NSE) Documentation](https://nmap.org/book/nse.html)

## Key Takeaways

- Enumeration is about triage: not every open port deserves equal attention up front.
- Anonymous FTP access was the standout lead, directly shaping the order of the following phases: FTP → Credentials → Initial Access → Privilege Escalation.
