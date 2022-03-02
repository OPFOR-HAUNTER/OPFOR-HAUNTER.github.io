---
layout: post
title: "HTB Starting Point - Tier 1 - Ignition"
date: 2022-03-01
categories: RedOps ctf HTB
tags: ctf htb RedOps writeup easy ignition php
---
<img src='/assets/img/ctf/htb/sp/tier1/ignition/ignition.PNG'/>

## Introduction

## Establishing a Connection & Initial Scan

Spawn the bastard and get vpn going.

I've confirmed the target is reachable with a `ping`.

Start the default `nmap` scan and let it run while we complete the tasklist.

<img src='/assets/img/ctf/htb/sp/tier1/1nmap.png'>

## The Tasklist

### Task 1
#### Which service version is found to be running on port 80?

Our scan above shows `nginx 1.14.2` on port 80. This is a webserver, so there is a webpage we can visit via a browser.

### Task 2
#### What is the 3-digit HTTP status code returned when you visit http://{machine IP}/?

Error code `302`. According to [this KB entry](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/302), this code indicates a redirect is in place.


### Task 3
#### What is the virtual host name the webpage expects to be accessed by?


### Task 4 
#### What is the full path to the file on a Linux computer that holds a local list of domain name to IP address pairs?

### Task 5
#### What is the full URL to the Magento login page?

### Task 6
#### What password provides access as admin to Magento?

### Task 7
####  Submit root flag

## Capturing the Flag

