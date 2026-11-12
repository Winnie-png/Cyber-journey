
# Cybersecurity Journey

A hands-on record of my cybersecurity learning journey, documenting tools, practical exercises, findings, and lessons learned.

## Day 1 — 12 November 2026

### Environment Setup

**Platform:** Android / Termux

**Tools installed and verified:**
- Python 3.13.13
- Nmap 7.99
- OpenSSH 10.3

All three tools were installed and confirmed working in Termux.

---

### First Network Scan — Basic Nmap Scan

**Target:** `scanme.nmap.org`

**Command used:**

```console
$ nmap scanme.nmap.org
```

**Scan details:**
- Resolved IPv4 address: `45.33.32.156`
- Host status: Up
- Latency: 0.37 seconds
- Scan duration: 64.13 seconds
- IPv6 address reported but not scanned: `2600:3c01::f03c:91ff:fe18:bb2f`

**Findings:**

| Port | State | Service |
|---|---|---|
| 22/tcp | Open | SSH |
| 80/tcp | Open | HTTP |
| 9929/tcp | Open | Nping-echo |

- 3 open TCP ports discovered.
- 997 TCP ports were closed.
- 1 host was up.

**What I learned:**
- How to perform a basic network scan using Nmap.
- How to identify open ports and associated services.
- The difference between open, closed, and filtered ports.
- How to interpret basic Nmap scan results.

---

### Second Network Scan — Service Version Detection

**Target:** `scanme.nmap.org`

**Command used:**

```console
$ nmap -sV -p 22,80 scanme.nmap.org
```

**Scan details:**
- Resolved IPv4 address: `45.33.32.156`
- Host status: Up
- Latency: 0.44 seconds
- Scan duration: 14.48 seconds
- IPv6 address reported but not scanned: `2600:3c01::f03c:91ff:fe18:bb2f`
- Scan type: Service version detection (`-sV`)
- Ports scanned: 22 and 80

**Findings:**

| Port | State | Service | Detected Software |
|---|---|---|---|
| 22/tcp | Open | SSH | OpenSSH 6.6.1p1 |
| 80/tcp | Open | HTTP | Apache httpd 2.4.7 |

**Additional service information:**
- Operating system indication: Linux / Ubuntu
- SSH protocol: Version 2.0
- CPE: `cpe:/o:linux:linux_kernel`

**What I learned:**
- How Nmap's `-sV` option identifies services and their software versions.
- How to specify individual ports using the `-p` option.
- How to identify software associated with open network ports.
- The difference between basic port scanning and service enumeration.
- Why service version information is useful during security reconnaissance.

**Important note:** Service version detection provides identification estimates based on network responses. It does not, by itself, establish that a service is vulnerable.

---

## Key Takeaways

- Successfully configured a cybersecurity learning environment in Termux.
- Installed and verified Python, Nmap, and OpenSSH.
- Performed a basic TCP port scan.
- Identified three open ports on Nmap's designated test host.
- Performed service version detection on SSH and HTTP.
- Practised interpreting network reconnaissance results.

## Next Learning Steps

- TryHackMe: Pre Security beginner exercises.
- OverTheWire: Bandit Level 0 → Level 1.
- Continue practising Linux commands and basic networking.
