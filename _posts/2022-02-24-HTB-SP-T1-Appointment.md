---
layout: post
title: "HTB Starting Point - Tier 1 - Appointment"
date: 2022-02-24
categories: RedOps ctf HTB
tags: ctf htb RedOps writeup easy injection sqli
---
<img src='/assets/img/ctf/htb/sp/tier1/appointment/appointment.PNG'/>

## Introduction

We have captured 5 flags from the Tier 0 series, and are on the 1st of the Tier 1 series. This box is an introduction into SQL database injection.

## Establishing a Connection & Intitial Scan

Spawn the bastard and get vpn going.

I've confirmed the target is reachable with a `ping`.


## The Tasklist

### Task 1
#### What does the acronym SQL stand for?

`SQL` is the abbreviation for `Structured Query Language`. Many variants of it are used in a sizeable portion of the internet's databases to store, organize, and poll data efficiently. The language syntax is simple and easy to learn. 

Here is a [primer to familiarize yourself](https://www.tutorialrepublic.com/sql-tutorial/).


### Task 2
#### What is one of the most common type of SQL vulnerabilities?

`SQL Injection` is a notorious attack in which input from an end-user is not sanitized correctly, and the input contains data that the server interprets as a query statement against the database.

For example, a website's login page would have fields for a user to enter **username** & **password**. If these two fields are not sanitized correctly, a malicious actor could enter a SQL command here instead of username/password. Entering "'Select * from Users;' could query the database table Users and show sensitive info, instead of allowing a user to login.

Relevant XKCD
<img src='/assets/img/ctf/htb/sp/tier1/appointment/bobbytables.png'/>
[source](https://xkcd.com/327/)


### Task 3
### What does PII stand for?

`PII` is short for `Personally Identifiable Information`. This data can include names, birthdays, addresses, etc. and is considered sensitive to any organization storing the data.

### Task 4 
#### What does the OWASP Top 10 list name the classification for this vulnerability?

Briefly, the `OWASP Top 10` list is a curated list of web vulnerabilities. In their own words:
> It represents a broad consensus about the most critical security risks to web applications.

In OUR words, this is a prime checklist of types of exloits we should check for. 

[The OWASP Top 10 list can be found here](https://owasp.org/Top10/). Injection is currently ranked #3 on the list.

`A03:2021-Injection`

### Task 5
#### What service and version are running on port 80 of the target?

We got this info from our initial scan. The answer is `Apache httpd 2.4.38 ((Debian))`.

`Apache` is a server application, like `Nginx` and `IIS`. 

### Task 6
#### What is the standard port used for the HTTPS protocol?

`443`

### Task 7
#### What is one luck-based method of exploiting login pages?

`Brute-forcing`, though I wouldn't say it's *all* luck-based. Given some knowledge of the target and enough time, luck gives way to persistence.

### Task 8
#### What is a folder called in web-application terminology?

`Directory`; you should know this from the `dir busting` we did back in [Tier 0's Preignition](https://opfor-haunter.github.io/posts/HTB-SP-T0-Preignition/).

### Task 9
####  Submit root flag

## Capturing the Flag

Speaking of `dir busting`, it's time to capture our flag. Since we know this is a webserver, it doesn't hurt to look for hidden directories/pages to start our attack.

`gobuster dir -u $target -w /usr/share/wordlists/dirb/common.txt`

<img src='/assets/img/ctf/htb/sp/tier1/3gobuster.png'/>

We have a few hits worth noting. Let's try and visit the `Login page` our `nmap` scan found earlier. Put the IP address in the browser:

<img src='/assets/img/ctf/htb/sp/tier1/2login.png'/>

We could try `bruteforcing` the login, but this server looks more configured than the last one. Let's try `SQL injection`.

My experience with `SQLi` is very limited, but there must be tools on Kali. 

`ls /bin/*sql*`

<img src='/assets/img/ctf/htb/sp/tier1/appointment/4sqltools.png'/>






