---
layout: post
title: "HTB Starting Point - Tier 0 - Fawn"
date: 2022-02-04
categories: RedOps ctf HTB
tags: ctf htb RedOps writeup easy fawn
---
<img src='/assets/img/ctf/htb/sp/tier0/fawn/fawn.PNG'/>

## Introduction

Fawn is the second in the Tier 0 Starting Point machines. This is another educational system, so I will cover the commands in-depth than I will in future machines, but will build off knowledge from the previous machine, Meow.

## Establishing a Connection

Spawn the bastard and get vpn going.

![The host machine IP](/assets/img/ctf/htb/sp/tier0/fawn/1ip.PNG)

I've confirmed the target is reachable with a `ping`.

## Initial Scan

Unlike the last machine, let's do our default `nmap` scan now and store the results in `recon/all` again and move on to the tasklist.

## The Tasklist

Now that we've established a connection, let's get started on the tasks. These tasks are meant to educate, so make sure you take the extra time to research more about any tasks you are unfamiliar with.

### Task 1
####  What does the acronym VM stand for?
**V**irtual **M**achine. You can read my VM config guide ![here]()

### Task 2
#### What tool do we use to interact with the operating system in order to start our VPN connection? 
The **Terminal**. You should be living and breathing inside a terminal everyday imo.

### Task 3
####What service do we use to form our VPN connection?
**Openvpn** 

### Task 4 
#### What is the abreviated name for a tunnel interface in the output of your VPN boot-up sequence output? 
**tun** is short for tunnel.

### Task 5
#### What tool do we use to test our connection to the target?
**ping**, we did this at the end of the connection section.

## Our First Scan
### Task 6
#### What is the name of the tool we use to scan the target's ports?
**nmap**, TryHackMe has a great room on this tool [here](https://tryhackme.com/room/furthernmap). This will be one of your most used tools, so get intimate with it!

### Task 7
#### What service do we identify on port 23/tcp during our scans?
We should run a default scan from now on once we've established network visibility, as we did earlier. We'll run the following nmap scan as a default:

`nmap -v -T4 -A -oA recon/all $target`

<img src='/assets/img/ctf/htb/sp/tier0/meow/4nmap.png' style='display:block;'/>

`-v`: enable verbose mode. Make this another habit so we always have more info.
`-T4`: time/throttle speed for the scan. Range is 0 to 5, with 0 being the slowest and 5 the fastest. Slow is more reliable & less 'loud', but can take a considerable amount of time. 5 is extremely fast, but can be inaccurate and trigger many IDS/IPS alerts.
`-oA recon/all`: This flag combined with A will output the scan results into files in folder 'recon'. This folder must exist before the scan is ran, and can also represent a full dir path. The A stands for 'all' and will create three files formatted each for nmap, xml, and gnmap. See the below image at #1.

<img src='/assets/img/ctf/htb/sp/tier0/meow/5nmap_resultscan.png' style='display:block;'/>

We can view the results by running the following command (above picture at #2):
`cat recon/all.nmap | less`
`cat`: This command outputs the contents of a file to the current terminal window. It does not knock stuff off tables without a reason.
`|`: The 'pipe' is a powerfull tool used to redirect the output of a command to the left `cat` in this instance) to a second command on the right (`less` in this instance).
`less`: This command let's us paginate output. This is handy, for example, if the contents of our nmap screen is too large to read on our current screen. Without `less`, we'd have to deal with scrolling through output we can be annoying in terminal. With `less`, we can go up and down the output using the `PGUP` and `PGDN` buttons respectively. Once you are done viewing, you can exit with the `q` button.

<img src='/assets/img/ctf/htb/sp/tier0/meow/5nmap_resuls.png' style='display:block;'/>

Here are our scan results. We can see that `telnet` is the service running on `port 23`.
## Attacking
### Task 8
### What username ultimately works with the remote management login prompt for the target?
If you have not used `telnet` before, run `man telnet` to see the syntax for the command.

`telnet $target` appears to be the basic syntax for attempting a connection. Let's give it a shot.

<img src='/assets/img/ctf/htb/sp/tier0/meow/6telnet.png' style='display:block;'/>

Great! The target is accepting attempts to authenticate. Below we try to connect without a username or password...but are shit out of luck.

For a first try, always try `root`. We try it here, and success:

<img src='/assets/img/ctf/htb/sp/tier0/meow/7telnet_con.png' style='display:block;'/>

### Task 9
####  Submit root flag
-Now that we are `in`, let's do a simple `**ls**` and we see our `flag.txt`. `cat` out the contents and you have gotten your first flag! 

<img src='/assets/img/ctf/htb/sp/tier0/meow/8.png' style='display:block;'/>

Note: my flag is blurred out as `sharing a flag is frowned upon`, not because it's full of f-bombs or similar.
