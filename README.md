# Offensive Security Knowledge Base

> A methodology-driven cybersecurity knowledge base built from personal lab notes, documenting reconnaissance, enumeration, and privilege escalation techniques against an intentionally vulnerable Linux target.

![Markdown](https://img.shields.io/badge/docs-Markdown-blue?logo=markdown)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-active-brightgreen)
![Focus](https://img.shields.io/badge/focus-Linux%20%7C%20Web%20%7C%20PrivEsc-orange)
![PRs](https://img.shields.io/badge/PRs-welcome-yellow)

## About This Repository

This repository is not a walkthrough. It is a structured knowledge base derived from real lab notes, terminal sessions, and screenshots, documenting the methodology behind each stage of a penetration test: reconnaissance, enumeration, web analysis, credential access, initial access, and privilege escalation.

Every command, output, and observation documented here was actually executed and captured. Nothing is fabricated. Where additional explanation is useful for learning purposes, it is clearly separated into an **Additional Context** section on each page.

> [!NOTE]
> This repository documents concepts, methodology, and commands executed against an isolated, intentionally vulnerable lab environment. It is intended for educational purposes and authorized security testing only.

## Table of Contents

- [About This Repository](#about-this-repository)
- [Repository Structure](#repository-structure)
- [Learning Objectives](#learning-objectives)
- [Topics Covered](#topics-covered)
- [Navigation](#navigation)
- [Cheat Sheets](#cheat-sheets)
- [Tools Used](#tools-used)
- [Repository Statistics](#repository-statistics)
- [Future Improvements](#future-improvements)
- [Acknowledgements](#acknowledgements)
- [License](#license)

## Repository Structure

```
.
├── README.md
├── LICENSE
├── .gitignore
│
├── docs/
│   ├── 01-Recon/                  # Host discovery and port scanning
│   ├── 02-Enumeration/            # Service enumeration and analysis
│   ├── 03-Web/                    # Web application review
│   ├── 04-FTP/                    # FTP service exploitation
│   ├── 05-Credentials/            # Credential discovery and cracking
│   ├── 06-Initial-Access/         # Gaining a foothold
│   └── 07-Privilege-Escalation/   # Escalating to root
│
├── cheatsheets/                   # Standalone quick-reference sheets
│   ├── nmap.md
│   ├── ffuf.md
│   ├── ftp.md
│   ├── hashcat.md
│   ├── netcat.md
│   ├── linux-enumeration.md
│   ├── privilege-escalation.md
│   └── reverse-shells.md
│
├── images/                        # Screenshots referenced across docs/
│
└── resources/                     # External references and further reading
```

## Learning Objectives

- Apply a structured, repeatable reconnaissance methodology
- Read and interpret Nmap service and version scans
- Enumerate anonymous FTP access for information disclosure
- Recognize credential leakage through exposed plaintext files
- Perform targeted password attacks against SSH with Hydra
- Establish initial access over SSH
- Audit sudo permissions (`sudo -l`) for privilege escalation paths
- Use GTFOBins to identify escalation techniques for permitted binaries
- Escalate from a restricted shell to root

## Topics Covered

| Category | Description |
|---|---|
| Reconnaissance | Host discovery (`ping`) and full-port service/version scanning (`nmap`) |
| Enumeration | Interpreting scan output and identifying attack surface |
| Web | Reviewing an exposed HTTP service |
| FTP | Anonymous FTP login and file retrieval |
| Credentials | Extracting leads from a discovered file and cracking SSH credentials |
| Initial Access | Authenticating over SSH with discovered credentials |
| Privilege Escalation | Sudo misconfiguration abuse via GTFOBins to obtain root |

## Navigation

| Section | Description |
|---|---|
| [01 – Recon](docs/01-Recon/README.md) | Initial host discovery and port scanning |
| [02 – Enumeration](docs/02-Enumeration/README.md) | Service enumeration and analysis |
| [03 – Web](docs/03-Web/README.md) | Web service review |
| [04 – FTP](docs/04-FTP/README.md) | Anonymous FTP access and file retrieval |
| [05 – Credentials](docs/05-Credentials/README.md) | Note analysis and credential brute force |
| [06 – Initial Access](docs/06-Initial-Access/README.md) | SSH foothold |
| [07 – Privilege Escalation](docs/07-Privilege-Escalation/README.md) | Sudo/GTFOBins root escalation |

## Cheat Sheets

| Cheat Sheet | Description |
|---|---|
| [Nmap](cheatsheets/nmap.md) | Scanning syntax, options, and common flags |
| [FFUF](cheatsheets/ffuf.md) | Web fuzzing syntax and options |
| [FTP](cheatsheets/ftp.md) | FTP client commands and enumeration tips |
| [Hashcat](cheatsheets/hashcat.md) | Hash cracking modes and syntax |
| [Netcat](cheatsheets/netcat.md) | Listener and connection syntax |
| [Linux Enumeration](cheatsheets/linux-enumeration.md) | Manual and automated Linux enumeration |
| [Privilege Escalation](cheatsheets/privilege-escalation.md) | Common Linux privesc vectors |
| [Reverse Shells](cheatsheets/reverse-shells.md) | Common reverse shell one-liners |

## Tools Used

| Tool | Purpose |
|---|---|
| `ping` | Host liveness check |
| `nmap` | Port scanning, service/version detection |
| `ftp` | Interacting with the FTP service |
| `hydra` | Online password brute forcing (SSH) |
| `ssh` | Remote authentication and shell access |
| `sudo -l` | Enumerating sudo privileges |
| GTFOBins | Reference for abusing allowed binaries |
| `less` | Abused via sudo for privilege escalation |

## Repository Statistics

| Metric | Value |
|---|---|
| Documentation sections | 7 |
| Cheat sheets | 8 |
| Screenshots documented | 10 |
| Services enumerated | FTP, SSH, HTTP |
| Outcome | Root access obtained |

## Future Improvements

- [ ] Add automated enumeration script references
- [ ] Expand the Web section with directory fuzzing results
- [ ] Add a dedicated Post-Exploitation section
- [ ] Include hash-cracking notes for future labs involving credential hashes
- [ ] Add diagrams illustrating the full attack chain

## Acknowledgements

- [HackTricks](https://book.hacktricks.wiki/) — structure and formatting inspiration
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings) — cheat sheet inspiration
- [GTFOBins](https://gtfobins.org/) — privilege escalation reference
- [OWASP](https://owasp.org/) — documentation style reference

## License

This project is licensed under the [MIT License](LICENSE).
