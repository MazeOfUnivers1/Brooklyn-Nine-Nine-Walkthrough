# FTP Cheat Sheet

## Overview

FTP (File Transfer Protocol) is a plaintext protocol used for transferring files between a client and server. Misconfigured FTP servers commonly allow anonymous access, which can expose sensitive files.

## Common Syntax

```bash
ftp <target>
```

## Useful Commands

```bash
# Connect to an FTP server
ftp <target>

# Login as anonymous (when prompted for username)
Anonymous

# List directory contents
ls -la

# Change remote directory
cd <directory>

# Download a file
get <filename>

# Download multiple files
mget *

# Upload a file (if write access is allowed)
put <filename>

# Switch to binary transfer mode
binary

# Exit the session
bye
```

## Important Options

| Command | Description |
|---|---|
| `Anonymous` / `anonymous` | Standard username for anonymous FTP login |
| `ls -la` | Lists all files, including hidden ones, with permissions |
| `get` | Downloads a single file |
| `mget` | Downloads multiple files matching a pattern |
| `put` | Uploads a file (requires write permission) |
| `binary` | Ensures accurate transfer of non-text files |

## Examples

```text
$ ftp 10.114.175.118
Connected to 10.114.175.118.
220 (vsFTPd 3.0.3)
Name (10.114.175.118:kali): Anonymous
331 Please specify the password.
Password:
230 Login successful.
```

Anonymous login accepted, allowing directory listing and file retrieval (as documented in [04-FTP](../docs/04-FTP/README.md)).

## Common Mistakes

- Forgetting to press Enter at the (blank) password prompt during anonymous login attempts.
- Not switching to binary mode before downloading non-text files, which can corrupt the transfer.
- Overlooking file ownership/permissions in directory listings, which can provide clues about the server's configuration.

## References

- [vsftpd Documentation](https://security.appspot.com/vsftpd.html)

## Key Takeaways

- Always test for anonymous access (`Anonymous` / blank password) on discovered FTP services.
- Directory listings can reveal filenames that hint at usernames or credentials before a single file is even opened.
