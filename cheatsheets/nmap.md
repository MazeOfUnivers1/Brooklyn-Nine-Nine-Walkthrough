# Nmap Cheat Sheet

## Overview

Nmap ("Network Mapper") is a network scanning tool used for host discovery, port scanning, service/version detection, OS fingerprinting, and scriptable interaction with services via the Nmap Scripting Engine (NSE).

## Common Syntax

```bash
nmap [scan type] [options] <target>
```

## Useful Commands

```bash
# Full TCP port range, version/OS detection, default scripts
nmap -A -p- -T3 <target>

# Fast scan of top 1000 ports
nmap <target>

# Scan specific ports
nmap -p 21,22,80 <target>

# UDP scan
nmap -sU <target>

# Scan with a specific NSE script
nmap --script ftp-anon <target>

# Save output in all formats
nmap -A -p- -oA scan_results <target>
```

## Important Options

| Option | Description |
|---|---|
| `-A` | Aggressive scan: OS detection, version detection, script scanning, traceroute |
| `-p-` | Scan all 65535 TCP ports |
| `-p <ports>` | Scan specific port(s) |
| `-sV` | Service/version detection |
| `-sС` | Run default NSE scripts |
| `-sU` | UDP scan |
| `-Pn` | Skip host discovery (treat host as online) |
| `-T0` – `-T5` | Timing template, from paranoid (0) to insane (5) |
| `-oA <basename>` | Output results in normal, XML, and grepable formats |
| `--script <name>` | Run a specific NSE script |

## Examples

```bash
sudo nmap -A -p- -T3 10.114.175.118
```

Runs an aggressive, full-port scan against the target, returning service versions and applicable NSE script output (as used in [01-Recon](../docs/01-Recon/README.md)).

## Common Mistakes

- Only scanning the default top 1000 ports and missing services on non-standard ports.
- Forgetting `sudo` for scan types requiring raw socket access (e.g., SYN scans, OS detection).
- Not reviewing NSE script output bundled into `-A`, which often reveals quick wins (e.g., anonymous FTP access).

## References

- [Nmap Official Documentation](https://nmap.org/book/man.html)

## Key Takeaways

- `-A -p-` is a strong default for thorough initial reconnaissance against a single target.
- Always review script output, not just the open port list.
