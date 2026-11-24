# Hashcat Cheat Sheet

## Overview

Hashcat is a GPU-accelerated password recovery tool supporting a wide range of hash types, used for offline cracking of captured hashes (as opposed to online brute forcing against a live service).

## Common Syntax

```bash
hashcat -m <hash-mode> -a <attack-mode> <hash-file> <wordlist>
```

## Useful Commands

```bash
# Dictionary attack against an MD5 hash
hashcat -m 0 -a 0 hashes.txt wordlist.txt

# Dictionary attack against a SHA-256 hash
hashcat -m 1400 -a 0 hashes.txt wordlist.txt

# Crack an SSH private key passphrase (after conversion with ssh2john)
hashcat -m 22921 -a 0 ssh_hash.txt wordlist.txt

# Brute-force (mask) attack
hashcat -m 0 -a 3 hashes.txt ?a?a?a?a?a?a

# Show already-cracked results
hashcat -m 0 hashes.txt --show
```

## Important Options

| Option | Description |
|---|---|
| `-m` | Hash type/mode (e.g., `0` = MD5, `1000` = NTLM, `1800` = sha512crypt) |
| `-a` | Attack mode (`0` = dictionary, `1` = combinator, `3` = brute-force/mask, `6`/`7` = hybrid) |
| `--show` | Displays previously cracked hashes from the potfile |
| `-r` | Applies a rule file to a dictionary attack |
| `-o` | Output file for cracked results |

## Examples

```bash
hashcat -m 0 -a 0 hashes.txt /usr/share/wordlists/rockyou.txt
```

Runs a straight dictionary attack against MD5 hashes using the common `rockyou.txt` wordlist.

## Common Mistakes

- Using the wrong `-m` hash mode identifier, which silently returns no results.
- Forgetting to unzip/prepare large wordlists (e.g., `rockyou.txt.gz`) before use.
- Not checking `--show` after a session, missing hashes that were already cracked in an earlier run.

## References

- [Hashcat Official Documentation](https://hashcat.net/wiki/)

## Key Takeaways

- Hash mode identification (`-m`) is the most critical and most commonly misconfigured part of a Hashcat command.
- Rule-based attacks (`-r`) can dramatically increase dictionary attack coverage without needing a larger wordlist.
