---
layout: post
title: "HTB Starting Point - Tier 1 - Bike"
date: 2022-03-03
categories: RedOps ctf HTB
tags: ctf htb RedOps writeup easy bike ssti injection proxy burpsuite
---
<img src='/assets/img/ctf/htb/sp/tier1/bike/bike.PNG'/>

## Introduction

This is the 5th target in the Tier 1 lineup, and the 2nd of 3 VIP machines. Ths machine introduces `SSTI` and the use of a `proxy` to conduct the attack.


## Establishing a Connection and Initial Scan

Spawn the bastard and get vpn going.

I've confirmed the target is reachable with a `ping`.

Start the default `nmap` scan and let it run while we complete the tasklist.

<img src='/assets/img/ctf/htb/sp/tier1/bike/1nmap.png'>

## The Tasklist

### Task 1
#### What TCP ports does nmap identify as open? Answer with a list of ports seperated by commas with no spaces, from low to high.

`22,80`

### Task 2
#### What software is running the service listening on the http/web port identified in the first question?

<img src='/assets/img/ctf/htb/sp/tier1/bike/1nmap.png'>

`node.js`

### Task 3
#### What is the name of the Web Framework according to Wappalyzer?
`express`


### Task 4 
#### What is the name of the vulnerability we test for by submitting`?
`Server Side Template Injection` aka `SSTI`
[SSTI Injection on HackTricks](https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection)

### Task 5
#### What is the templating engine being used within Node.JS?
`Handlebars`
[Handlebars Template Injection Payload on HackTricks](https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection#handlebars-nodejs)



### Task 6
#### What is the name of the BurpSuite tab used to encode text?
`decoder`


### Task 7
#### In order to send special characters in our payload in an HTTP request, we'll encode the payload. What type of encoding do we use?
`url`


### Task 8
#### When we use a payload from HackTricks to try to run system commands, we get an error back. What is "not defined" in the response error?
`require`


### Task 9
#### What variable is the name of the top-level scope in Node.JS?
`global`

### Task 10
####  By exploiting this vulnerability, we get command execution as the user that the webserver is running as. What is the name of that user?
`root`

## Capturing the Flag

