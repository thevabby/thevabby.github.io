---
title: Nmap - CheatSheet
date: 2023-09-04 11:11:11 -001
categories: [NMAP, nmap]
tags: [nmap]
---

## NMAP Commands

#### Store output in normal format using -oN flag

    ```bash
    nmap -p80 -sC -sV scanme.nmap.org -oN output.txt
    ```

#### Syn scan with -sS flag and UDP scan with -sU flag

    ```bash
    nmap -p80 -sS scanme.nmap.org
    nmap -p80 -sU scanme.nmap.org
    ```


#### nmap scripts - /usr/share/nmap/scripts

some script categories are safe, intrusive, vuln, exploit, auth, brute, discovery

We can search script in /usr/share/nmap/scripts and use help using "nmap --script-help <script-name>"

```bash
nmap -p80 -sV --script=vuln scanme.nmap.org
```

#### For ping sweep across a network using CIDR notation
switch -sn is for ping sweep (ICMP)

```bash
nmap -sn 172.16.0.0/16
```
