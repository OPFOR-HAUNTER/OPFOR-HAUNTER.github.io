---
layout: post
title: "HTB Starting Point - Tier 0 - Preignition"
date: 2022-02-22
categories: RedOps ctf HTB
tags: ctf htb RedOps writeup easy preignition webenum dirbuster gobuster
---
<img src='/assets/img/ctf/htb/sp/tier0/preignition/preignition.PNG'/>

## Introduction

Preignition is the final box in the Tier 0 series, and the 2nd of 2 VIP machines. This lab focuses on web enumeration/dir busting.

## Establishing a Connection & Initial Scan

Spawn the bastard and get vpn going.

I've confirmed the target is reachable with a `ping`.

As with all other labs to now, start a scan and let it cook while we do the boring task stuff.

`nmap -v -T4 -A -oA recon/all $target`

<img src='/assets/img/ctf/htb/sp/tier0/preignition/1nmap.png'>

## The Tasklist

### Task 1
#### What is considered to be one of the most essential skills to possess as a Penetration Tester?

The answer is `dir busting`, short for *directory busting*. This is an active recon technique that targets web servers with the intent of discovering directories/pages for potential exploitation.

### Task 2
#### What switch do we use for nmap's scan to specify that we want to perform version detection

`man nmap` shows us the following regarding version detection:

<img src='/assets/img/ctf/htb/sp/tier0/preignition/2version.png'/>

The switch in question is `-sV`.

> Note: the `-A` switch we have been using in our default scan includes version detection as well. However, `-A` contains other utilities that may be overkill for targeted scans. In those instances, specifying `-sV` for version detection would be more streamlined if that's all that is needed.

### Task 3
### What service type is identified as running on port 80/tcp in our nmap scan?

Our results show `http` is running on `80/tcp`.

### Task 4 
#### What service name and version of service is running on port 80/tcp in our nmap scan?

Results show the service name/version is `nginx 1.14.2`.

`nginx` is commonly used as a webserver solution. You can read moar about it [here](https://en.wikipedia.org/wiki/Nginx).


### Task 5
#### What is a popular directory busting tool we can use to explore hidden web directories and resources?

We can see what's currently installed on Kali as we did before by searching `/bin/` for the term `"bust"`

<img src='/assets/img/htb/sp/tier0/preignition/3lsbust.png'/>

There are two options here:
1. `dirbuster`
2. `gobuster`

There are of course more options that are popular as well. For this lab, however, the answer will be `gobuster`.

### Task 6
#### What switch do we use to specify to gobuster we want to perform dir busting specifically?

Let's check with `man gobuster` WAIT VAT ZE FECK? 

<img src='/assets/img/htb/sp/tier0/preignition/4gobusterhelp.png'/>

1. `gobuster` doesn't have a man page! :(
2. Luckily, `--help` is always a viable alternative. You can also reference [this site](https://linuxcommandlibrary.com/man/gobuster) for man pages for tools.
3. Now that we can see the tool's syntax, we see that `dir` is the switch we need to include in our command for dir busting.
4. Take note that we can get specific command syntax with the formatting listed here. Example, `gobuster dir --help` will get you the specifc help page with additional `dir` details (see below image).

<img src='/assets/img/htb/sp/tier0/preignition/4gobusterhelp2.png'/>

### Task 7
#### What page is found during our dir busting activities?



### Task 8
#### What is the status code reported by gobuster upon finding a successful page?

### Task 9
####  Submit root flag

## Capturing the Flag

