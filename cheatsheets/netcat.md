# Netcat Cheat Sheet

## Overview

Netcat (`nc`) is a versatile networking utility used for reading and writing data across network connections — commonly used for banner grabbing, port scanning, file transfers, and setting up reverse/bind shells.

## Common Syntax

```bash
nc [options] <target> <port>
```

## Useful Commands

```bash
# Connect to a service (banner grabbing)
nc -nv <target> <port>

# Start a listener
nc -lvnp <port>

# Send a file
nc -nv <target> <port> < file.txt

# Receive a file
nc -lvnp <port> > received_file.txt

# Simple port scan
nc -zv <target> 1-1000
```

## Important Options

| Option | Description |
|---|---|
| `-l` | Listen mode (start a listener rather than connecting out) |
| `-v` | Verbose output |
| `-n` | Skip DNS resolution (numeric IPs only) |
| `-p` | Specify local port to use/listen on |
| `-z` | Zero-I/O mode, used for port scanning |
| `-e` | Execute a program upon connection (legacy; often removed in modern builds for security reasons) |

## Examples

```bash
nc -lvnp 4444
```

Starts a listener on port 4444 to catch an incoming reverse shell connection.

## Common Mistakes

- Forgetting to start the listener before triggering a reverse shell payload, resulting in a missed connection.
- Using a port already in use or blocked by a firewall on the attacking machine.
- Relying on `-e` for shell execution when the local Netcat build doesn't support it (common on modern Linux distributions).

## References

- [Netcat Manual Page](https://man7.org/linux/man-pages/man1/ncat.1.html)

## Key Takeaways

- Netcat is a foundational tool for catching reverse shells and performing quick connectivity/banner checks.
- Always confirm the listener is active and the correct port is open/forwarded before triggering a payload.
