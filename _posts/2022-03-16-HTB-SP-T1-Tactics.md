---
layout: post
title: "HTB Starting Point - Tier 1 - Tactics"
date: 2022-02-24
categories: RedOps ctf HTB
tags: ctf htb RedOps writeup easy tactics smb
---
<img src='/assets/img/ctf/htb/sp/tier1/tactics/tactics.PNG'/>


# collapsible section with markdown
<details>
  <summary>Click to expand!</summary>
  
  ## Heading
  1. A numbered
  2. list
     * With some
     * Sub bullets
</details>

## Introduction

## Establishing a Connection & Initial Scan

Spawn the bastard and get vpn going.

I've confirmed the target is reachable with a `ping`.

Start the default `nmap` scan and let it run while we complete the tasklist.

<img src='/assets/img/ctf/htb/sp/tier1/1nmap.png'>



## The Tasklist

### Task 1
#### Which Nmap switch can we use to enumerate machines when our packets are otherwise blocked by the Windows firewall?

`nmap -Pn -A -v -T4 -oA recon/all $target`

### Task 2
#### What does the 3-letter acronym SMB stand for?

### Task 3
#### What port does SMB use to operate at?

### Task 4 
#### What command line argument do you give to `smbclient` to list available shares?

### Task 5
#### What character at the end of a share name indicates it's an administrative share?

### Task 6
#### Which Administrative share is accessible on the box that allows users to view the whole file system?

### Task 7
#### What command can we use to download the files we find on the SMB Share?


### Task 8
#### Which tool that is part of the Impacket collection can be used to get an interactive shell on the system?

### Task 9
####  Submit root flag

## Capturing the Flag

