# FFUF Cheat Sheet

## Overview

`ffuf` (Fuzz Faster U Fool) is a fast web fuzzer used for directory/file discovery, virtual host discovery, and parameter fuzzing.

## Common Syntax

```bash
ffuf -w <wordlist> -u <url with FUZZ keyword> [options]
```

## Useful Commands

```bash
# Directory/file discovery
ffuf -w /usr/share/wordlists/dirb/common.txt -u http://target/FUZZ

# Filter by file extension
ffuf -w wordlist.txt -u http://target/FUZZ -e .php,.txt,.html

# Virtual host discovery
ffuf -w subdomains.txt -u http://target/ -H "Host: FUZZ.target.com"

# Filter out a specific response size (reduce false positives)
ffuf -w wordlist.txt -u http://target/FUZZ -fs 1234

# POST parameter fuzzing
ffuf -w wordlist.txt -u http://target/login -X POST -d "user=admin&pass=FUZZ" -H "Content-Type: application/x-www-form-urlencoded"
```

## Important Options

| Option | Description |
|---|---|
| `-w` | Path to the wordlist |
| `-u` | Target URL, with `FUZZ` marking the injection point |
| `-e` | Comma-separated list of extensions to append |
| `-fs` | Filter responses by size |
| `-fc` | Filter responses by HTTP status code |
| `-mc` | Match responses by HTTP status code |
| `-H` | Add a custom header |
| `-X` | HTTP method (e.g., `POST`) |
| `-d` | Request body data |
| `-t` | Number of concurrent threads |

## Examples

```bash
ffuf -w /usr/share/wordlists/dirb/common.txt -u http://10.114.175.118/FUZZ
```

Performs directory/file discovery against the target's web root using a common wordlist.

## Common Mistakes

- Not filtering out the "default" response size/status, resulting in noisy output full of false positives.
- Forgetting the `FUZZ` keyword in the URL, causing `ffuf` to fail silently or fuzz the wrong location.
- Using an overly large wordlist without adjusting thread count, causing excessive scan time.

## References

- [FFUF GitHub Repository](https://github.com/ffuf/ffuf)

## Key Takeaways

- Always filter noisy/default responses (`-fs`/`-fc`) to keep output readable.
- `ffuf` is versatile beyond directory brute forcing — it also supports vhost and parameter fuzzing.
