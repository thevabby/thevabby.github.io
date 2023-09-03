---
title: TryHackMe - Kenobi
date: 2023-09-02 11:11:11 -001
categories: [TryHackMe, THM]
tags: [thm, kenobi]
---

# Kenobi

### nmap scripts to scan SMB

``` nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.253.48 ```

### nmap scripts to scan RPC

nmap port scan will show port 111 running the service rpcbind. This is just a server that converts remote procedure call (RPC) program number into
universal addresses. When an RPC service is started, it tells rpcbind the address at which it is listening and the RPC program number its prepared to serve.

In our case, port 111 is access to a network file system. Lets use nmap to enumerate this.

``` nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.253.48 ```

---
### SUID

SUID bits can be dangerous, some binaries such as passwd need to be run with elevated privileges (as its resetting your password on the system), however other custom files could that have the SUID bit can lead to all sorts of issues.

To search the a system for these type of files run the following: find / -perm -u=s -type f 2>/dev/null


``` find / -perm -u=s -type f 2>/dev/null ```