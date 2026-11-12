
# Cybersecurity Journey

A hands-on record of my cybersecurity learning journey, labs, tools, and practical exercises.

## Day 1 — 12 November 2026

### Environment
- Platform: Android / Termux
- Python: 3.13.13
- Nmap: 7.99
- OpenSSH: 10.3

All three tools were installed and their versions verified successfully.

### First Network Scan

**Target:** `scanme.nmap.org`  
**Resolved IPv4:** `45.33.32.156`  
**Scan time:** 19:12 (+0300)  
**Host status:** Up  
**Latency:** 0.37 seconds  
**Scan duration:** 64.13 seconds

#### Results

| Port | State | Service |
|---|---|---|
| 22/tcp | Open | SSH |
| 80/tcp | Open | HTTP |
| 9929/tcp | Open | nping-echo |

- 997 closed TCP ports were not displayed.
- One IPv4 address was scanned.
- An additional IPv6 address was reported but not scanned.

#### Command

```console
$ nmap scanme.nmap.org
```

### What I Learned
- How to verify installed cybersecurity tools.
- How to run a basic Nmap scan.
- How to identify open ports and associated services.
- How to interpret basic host and scan information.

### Next Steps
- Begin beginner-friendly TryHackMe labs.
- Start OverTheWire Bandit.
- Continue practising network reconnaissance in authorised environments.
