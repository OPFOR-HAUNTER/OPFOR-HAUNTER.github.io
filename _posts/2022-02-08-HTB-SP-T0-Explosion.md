---
layout: post
title: "HTB Starting Point - Tier 0 - Explosion"
date: 2022-02-08
categories: RedOps ctf HTB
tags: ctf htb RedOps writeup easy explosion rdp
---
<img src='/assets/img/ctf/htb/sp/tier0/explosion/explosion.PNG'/>

## Introduction

Explosion is the 4th system in the Tier 0 list, and the 1st of 2 VIP machines. `RDP` is the service theme here. 


## Establishing a Connection

Spawn the bastard and get vpn going.

I've confirmed the target is reachable with a `ping`.

## Initial Scan

`nmap -v -T4 -A -oA recon/all $target`
<img src='/assets/img/ctf/htb/sp/tier0/explosion/1nmap.png'/>


## The Tasklist

### Task 1
#### What does the 3-letter acronym RDP stand for?

`RDP` is short for **R**emote **D**esktop **P**rotocol. You can read moar about `RDP` <a href='https://www.ericom.com/whatis/rdp/#:~:text=RDP%20(Remote%20Desktop%20Protocol)%20is,ITU%20(International%20Telecommunications%20Union).'>here</a>.

### Task 2
#### What is a 3-letter acronym that refers to interaction with the host through a command line interface?

**C**ommand **L**ine **I**nterface is abbreviated to `cli`. The terminal window seen in most of my screenshots is a `cli` (see-el-eye).


### Task 3
### What about graphical user interface interactions?

Similary, **G**raphical **U**ser **I**nterface is abbreviated to `gui` (goo-ee). Any program that utilzes preset menus / buttons in a visual manner, rather that terminal input, is using a `gui`.


### Task 4 
#### What is the name of an old remote access tool that came without encryption by default?

If you recall [Meow](https://opfor-haunter.github.io/posts/HTB-SP-T0-meow/), we used the `telnet` tool to connect to the target. `telnet` used to transmit data in-the-clear out of the box. Anyone that would be capturing packets would be able to see all data being transmitted...including passwords.


### Task 5
#### What is the concept used to verify the identity of the remote host with SSH connections?

`public-key cryptography`

### Task 6
#### What is the name of the tool that we can use to initiate a desktop projection to our host using the terminal?

`xfreerdp`

### Task 7
#### What is the name of the service running on port 3389 TCP?

`ms-webt-server`

### Task 8
#### What is the switch used to specify the target host's IP address when using xfreerdp?

### Task 9
####  Submit root flag

## Capturing the Flag

