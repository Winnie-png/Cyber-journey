
# Cybersecurity Journey

A hands-on record of my cybersecurity learning journey. This repository documents my practical exercises, tools, findings, mistakes, and progress as I build foundational security skills.

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
- Ports examined: 22 and 80

**Findings:**

| Port | State | Service | Detected Software |
|---|---|---|---|
| 22/tcp | Open | SSH | OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 |
| 80/tcp | Open | HTTP | Apache httpd 2.4.7 |

**Additional service information:**
- Operating system indication: Linux / Ubuntu
- SSH protocol: Version 2.0
- CPE: `cpe:/o:linux:linux_kernel`

*Note: Service version detection identifies software based on network responses. The results are useful for reconnaissance but do not independently establish that a service is vulnerable.*

---

### Personal Reflection

**What surprised me**

My first scan took 64.13 seconds, which was longer than I expected. The second scan took just 14.48 seconds. I also found it interesting that Nmap could identify the software versions behind the SSH and HTTP services, rather than simply telling me which ports were open.

**What I'd do differently next time**

My second scan only examined ports 22 and 80, even though my first scan had identified three open ports. Next time, I'll include port 9929 in the follow-up scan so I can investigate all three services.

I also want to understand what the detected software versions mean from a security perspective, rather than assuming that an older version automatically means a vulnerability exists.

**Why I'm doing this**

I'm building practical cybersecurity skills from the ground up, with the goal of progressing towards a cybersecurity engineer role. I'm using hands-on exercises and documenting my progress so I can demonstrate what I've learned, not just what I've studied.

---

## Next Learning Steps

- TryHackMe: Pre Security beginner exercises.
- OverTheWire: Bandit Level 0 → Level 1.
- Continue practising Linux commands, networking fundamentals, and service enumeration.
