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

### Day 2 — TryHackMe: Offensive Security Intro

Date: 13 November 2026
Learning path: Cyber Security 101
Room: "Offensive Security Intro" (https://tryhackme.com/room/offensivesecurityintro)
Status: Completed

### What I did

Today I worked through the Offensive Security Intro room on TryHackMe.

I started by learning the difference between offensive and defensive security. Then I launched the FakeBank exercise and explored the simulated banking website.

The part that stood out was finding hidden pages. I used "dirb" for the first time to scan "http://fakebank.thm" for directories and files that weren't linked on the website.

The scan revealed two URLs. One of them was "/bank-transfer". I opened it, followed the exercise instructions and completed the challenge by making the required transfer in the simulated environment.

### What was new to me

I'd never used "dirb" before. This was my first practical experience with directory enumeration.

I also got to see why leaving sensitive functionality accessible without proper access controls is a problem. A page being difficult to find doesn't mean it's protected.

### My takeaway

I went into this exercise not knowing what DIRB was. I came out having used it to find a page I wouldn't have found through normal website navigation.

I want to understand what happens behind the scenes when DIRB scans a website, particularly how it uses wordlists and interprets the server's responses.

### Further exploration

After completing the room, I looked into how DIRB works behind the scenes. I learned how it uses wordlists to construct possible URLs, sends HTTP requests to the website and examines the responses to identify existing paths.

This helped me understand what was happening during the scan rather than just knowing which command to run.


## OverTheWire: Bandit — Initial Attempt

### What I did

I attempted OverTheWire: Bandit and progressed to Level 4. However, I was relying heavily on Claude to provide commands because I didn't fully understand what the exercises were teaching or what the commands were doing.

I realised I was copying commands without understanding them, so I decided to pause and work on the basics first.

### Where I got stuck

At that point, the commands I could confidently remember were `ls` and `mkdir`. I wasn't comfortable navigating directories or understanding file paths yet.

### What I'm doing differently

I've gone back to practising Linux commands in Termux, starting with:

- `pwd` — to see my current working directory.
- `ls` — to list files and directories.
- `cd` — to move between directories.
- `cd ..` — to move up one directory level.

I want to understand how directories and paths work before returning to Bandit and attempting the levels again.


## Day 3 — 16 November 2026

### TryHackMe: Defensive Security Intro

**Learning path:** Cyber Security 101  
**Room:** [Defensive Security Intro](https://tryhackme.com/room/defensivesecurityintro)  
**Status:** Completed (100%)

### What I did

I worked through a simulated SOC investigation at FakeBank involving suspicious login attempts.

The exercise introduced how a SOC uses monitoring dashboards to observe day-to-day activity across a system and build a picture of what normal behaviour looks like. When activity deviates from that baseline, it can trigger an alert for the SOC team to investigate.

I reviewed a Suspicious Login alert on the dashboard and identified the targeted username, `dave.saunders`.

I then disabled the account through the Account Management section. I also searched for the ShadowFigures threat group and updated the threat intelligence report with details of the targeted login page and username.

Finally, I submitted an incident report documenting the activity.

### What stood out to me

I hadn't thought much about how important it is to understand normal system activity before trying to identify suspicious behaviour.

An unusual event doesn't automatically tell an analyst what has happened. The alert is a starting point for investigation, not necessarily proof of an attack.

This was quite different from the Offensive Security Intro room. Instead of looking for weaknesses, I was working through the defender's side: monitoring activity, investigating an alert, taking action and documenting the incident.


### TryHackMe: Search Skills

**Learning path:** Cyber Security 101  
**Room:** [Search Skills](https://tryhackme.com/room/searchskills)  
**Status:** Completed (100%)

#### What I did

I explored several resources used in cybersecurity research and investigation through five practical exercises:

- **Shodan:** Searched for Apache servers using the TryScanMe simulation and identified the domain associated with a given IP address.
- **VirusTotal:** Checked a simulated suspicious file, `invoice_payment.exe`, and found that 52 security vendors had flagged it as dangerous.
- **CVE database:** Looked up `CVE-2026-1337` and reviewed its vulnerability details and CVSS classification.
- **Linux MAN pages:** Used the simulated manual pages to look up Netcat (`nc`) and find an example command for connecting to a host on a specified port.
- **GitHub:** Reviewed a repository containing information about a fictional CVE and located the script used to demonstrate the vulnerability.

#### What stood out to me

I hadn't realised how many specialised resources are available for cybersecurity research.

Each serves a different purpose. Shodan helps reveal information about internet-connected systems, VirusTotal provides a way to check suspicious files, and CVE databases help researchers identify and understand known vulnerabilities.

I also learned that technical documentation is available directly through Linux manual pages. Instead of relying entirely on tutorials, I can use `man` to look up how a command works and see its available options and examples.

The GitHub exercise also highlighted something important: finding a proof-of-concept script doesn't mean it is safe to run. Repositories need to be reviewed before executing their code.

#### What I learned

Knowing where to find reliable technical information is an important part of cybersecurity. I now have a better idea of where to look when researching suspicious files, identifying vulnerabilities, understanding command-line tools and investigating security-related code.



### Linux Fundamentals 1

**Date:** 18 November 2026

#### What I learned and practised

I worked through basic Linux commands using Termux and connected to a Linux virtual machine from my mobile phone using OpenConnect.

Commands I learned and used:

- `whoami` — displays the current username.
- `echo` — prints text to the terminal.
- `ls` — lists files and directories.
- `cat` — displays file contents.
- `cd` — changes directories.
- `pwd` — shows the current working directory.
- `find` — searches for files and directories.
- `grep` — searches for matching text in files.

#### Shell operators

I also learned about shell operators, including:

- `>` — redirects output to a file, replacing its existing contents.
- `>>` — redirects output to a file by appending to its existing contents.
- `&&` — runs the next command only if the previous command succeeds.
- `&` — runs a command in the background.

I practised output redirection with:

```bash
echo "TryHackMe" > thm
echo thm >> thm
cat thm
```

This helped me understand the difference between overwriting a file and appending new content.

#### What stood out to me

I have been learning Linux through my Android phone using Termux, and connecting to a Linux VM remotely made the experience even more interesting. I can now work with a Linux environment without needing a laptop.

I'm building my understanding of the terminal one command at a time.



## Day 4 — 19 November 2026

### Linux Fundamentals — Filesystem Navigation and File Inspection

#### What I practised

Today I focused on understanding how Linux organises files and directories, and how to navigate the filesystem using the terminal.

I used `pwd` to identify my current working directory:

```bash
pwd
```

In Termux, the output was:

```text
/data/data/com.termux/files/home
```

I practised navigating directories using:

```bash
cd ..
cd home
cd .ssh
cd ~
```

I learned that:

- `/` represents the root directory.
- `.` represents the current directory.
- `..` represents the parent directory.
- `~` is shorthand for my home directory.

I also used `ls` and `ls -la` to inspect the contents of my home directory.

The `-la` options showed hidden files and directories, along with their permissions and other details.

One thing I learned to recognise in the output:

- `d` at the beginning of a listing indicates a directory.
- `-` at the beginning indicates a regular file.
- Names beginning with `.` are hidden by default.

#### Reading files

I used the following commands to inspect files:

```bash
cat scan2.txt
head scan2.txt
tail scan2.txt
```

I revisited my saved Nmap scan output using `cat`.

I also learned that `head` displays the beginning of a file, while `tail` displays the end. This is useful when I don't need to read an entire file.

I was introduced to `tail -f`, which can follow a file as new lines are added. This is particularly useful when monitoring log files.

### OverTheWire — Bandit Practice

I continued practising Bandit and revisited earlier levels to strengthen my understanding.

#### Files with special names

In one challenge, I encountered a file whose name was simply `-`.

The command that worked was:

```bash
cat ./-
```

I learned that `./` specifies a path relative to the current directory. It also prevents a filename beginning with a hyphen from being interpreted as a command option.

#### Spaces in filenames

I explored how Linux handles filenames containing spaces.

The shell normally treats spaces as separators between arguments. I learned that I can escape spaces using a backslash:

```bash
cat incident\ report\ 2026.txt
```

Alternatively, I can enclose the filename in quotes:

```bash
cat "incident report 2026.txt"
```

#### Identifying file types — Bandit Level 4 to 5

I entered the `inhere` directory and found several files with names beginning with a hyphen.

I initially tried:

```bash
file *
```

This produced errors because the filenames beginning with `-` were interpreted as command options.

I then tried:

```bash
file ./*
```

This worked because the `./` prefix prevented the filenames from being interpreted as options.

The `file` command examines file contents to identify their types. Most of the files were identified as `data`, but one stood out:

```text
./-file07: ASCII text
```

I identified `./-file07` as the file to investigate and read its contents:

```bash
cat ./-file07
```

This revealed the password for `bandit5`. I successfully completed **Bandit Level 4 → 5**.

### What stood out to me

I'm starting to understand that Linux commands are not just isolated instructions. The way paths, filenames and command arguments are interpreted matters.

For example, `file *` and `file ./*` look almost identical, but they behave differently when filenames begin with a hyphen.

I also enjoyed learning how to inspect directories and understand what the terminal is showing me instead of just navigating blindly.

### What I want to practise next

- `grep` — searching for specific text inside files.
- `find` — locating files and directories.
- Linux file permissions.
- Reading and understanding system logs.
- Continue with OverTheWire Bandit Level 5 → 6.

I want to keep practising these fundamentals before moving on to more advanced security tools.


## Day 9 — Linux Fundamentals Part 2 & Bandit Levels 5–6

### Linux practice in Termux

Continued learning Linux fundamentals using Termux as a free alternative to the locked TryHackMe Linux Fundamentals Part 2 room.

Topics covered:
- Command arguments and options
- Users, UIDs and GIDs
- Groups and group membership
- Directory permissions vs file permissions
- Reading permission strings
- `chmod` using numeric permissions

Practised changing directory permissions using:

```bash
chmod 755 permissions_practice
chmod 740 permissions_practice
```

I learned that execute permission means something different depending on whether it's applied to a directory or a file:
- On a directory, it allows access or traversal.
- On a file, it allows you to run the program as a file.

### OverTheWire Bandit

**Level 5 → 6**

Searched through the `maybehere` directories to identify the file that matched the challenge requirements.

The file had to meet three conditions:
- It had to be human-readable.
- It had to be exactly 1,033 bytes.
- It could not be executable.

I used this command to narrow down the search by file size:

```bash
find . -type f -size 1033c
```

Breaking down the command:
- `find` — searches for files and directories.
- `.` — starts the search from my current directory.
- `-type f` — limits the results to regular files.
- `-size 1033c` — finds files that are exactly 1,033 bytes.
- `c` — specifies that the size is measured in bytes.

The command helped narrow down the files I needed to inspect. However, it only checked the file type and size. It did not check whether a file was human-readable or executable. I needed to use the other challenge clues to identify the correct file.

This level helped me understand that `find` can filter files by specific characteristics, reducing the amount of manual checking.

**Level 6 → 7**

Searched across the filesystem for a file matching specific ownership, group and size requirements.

```bash
find / -user bandit7 -group bandit6 -size 33c
```

The matching password file was:

```text
/var/lib/dpkg/info/bandit7.password
```

### What was new to me

- `find` can filter files based on ownership using `-user`.
- `find` can filter files based on group ownership using `-group`.
- Searching from `/` means searching throughout the filesystem rather than just the current directory.
- `2>/dev/null` redirects error messages so they don't clutter the search output.

I realised that I knew how to use `find` to list files, but I hadn't yet learned how to combine search criteria to narrow down the results.

### What I want to understand better

- Linux file searching and filtering
- Shell redirection, particularly `stderr` and `/dev/null`
- File management commands
- How to construct search commands independently instead of copying solutions
- 

