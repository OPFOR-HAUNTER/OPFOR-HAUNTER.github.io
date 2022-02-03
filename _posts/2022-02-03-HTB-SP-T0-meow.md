---
layout: post
title: "HTB Starting Point - Tier 0 - Meow"
date: 2022-02-03
categories: RedOps ctf HTB
tags: ctf htb RedOps writeup easy
---
<img src='/assets/ctf/htb/sp/tier0/meow/_meow.PNG'/>

## Introduction

As this is the first in a series of introductory HTB Starting Point machines, I will take extra time covering commands and terms. This will not continue in further writeups because, well that would be boring af.

So let's begin.

### Establishing a Connection

Let's spawn the machine and launch our local vpn client:

<img src='/assets/img/ctf/htb/sp/tier0/meow/_1ovpn.png'/>
`sudo openvpn /path/to/your/file.ovpn`

Now let's confirm we can see the machine with a ping.

Set the machine's IP to a variable first. You'll want to make this a habit :)

![](/assets/img/ctf/htb/sp/tier0/meow/_2ip.PNG)


<img src='/assets/img/ctf/htb/sp/tier0/meow/_3ping.png'/>

### The Tasklist

Now that we've established a connection, let's get started on the tasks. These tasks are meant to educate, so make sure you take the extra time to research more about any tasks you are unfamiliar with.

1. What does the acronym VM stand for?
	-**V**irtual **M**achine. You can read my VM config guide ![here]()
2. What tool do we use to interact with the operating system in order to start our VPN connection? 
	-The **Terminal**. You should be living and breathing inside a terminal everyday imo.
3. What service do we use to form our VPN connection?
	-**Openvpn** 
4. What is the abreviated name for a tunnel interface in the output of your VPN boot-up sequence output? 
	-**tun** is short for tunnel.
5. What tool do we use to test our connection to the target?
	- **ping**, we did this at the end of the connection section.
6. What is the name of the tool we use to scan the target's ports?
	-**nmap**, TryHackMe has a great room on this tool ![here](https://tryhackme.com/room/furthernmap). This will be one of your most used tools, so get intimate with it!
7. What service do we identify on port 23/tcp during our scans?
	-**telnet**
8. What username ultimately works with the remote management login prompt for the target?
	-**root**
9. Submit root flag
	-do the needful

