---
layout: post
title: "HTB Starting Point - Tier 1 - Pennywoth"
date: 2022-03-10
categories: RedOps ctf HTB
tags: ctf htb RedOps writeup easy pennyworth reverseshell bruteforce msf
---
<img src='/assets/img/ctf/htb/sp/tier1/pennyworth/pennyworth.PNG'/>

## Introduction

Pennyworth is the 6th machine in the Tier 1 group, and the 3rd VIP box. The focus of this box is webapp bruteforcing and establishing a reverse shell.

## Establishing a Connection & Initial Scan

Spawn the bastard and get vpn going.

I've confirmed the target is reachable with a `ping`.

Start the default `nmap` scan and let it run while we complete the tasklist.

<img src='/assets/img/ctf/htb/sp/tier1/1nmap.png'>

## The Tasklist

### Task 1
#### What does the acronym CVE stand for?
`Common Vulnerabilities and Exposures`

### Task 2
#### What do the three letters in CIA, referring to the CIA triad in cybersecurity, stand for?
`Confidentiality, Integrity, Availability`


### Task 3
#### What is the version of the service running on port 8080?
`Jetty 9.4.39.v20210325`, per our `nmap` scan results.


### Task 4 
#### What version of Jenkins is running on the target?
Evidently this information is available inside the webconsole after a successful login.

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/2jenkins.png "/>

We can navigate to the login page in-browser at `port 8080` (again per the `nmap` results).

According to the box writeup, the writer just brutforced the login creds by hand. That seemed a bit lame so I took this as an opportunity to learn a tool to do some automated bruteforcing.

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/3msf.png "/>

I tried `hydra` again but could not get it to work with this webapp. I switched to `metasploit` with `msfconsole`.

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/3msfsearcg.png "/>

Firstly, I ran `search jenkins` to verify if there were even any payloads available to target Jenkins. There were actually a few available and module 3 looked very promising.

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/3msfuse.png "/>

I seleced the module with `use 3`, and then took a look at the options with `show info`. Some options clearly reference bruteforce settings, so I went with this module.

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/3msfoptions.png "/>

There were a few options that were required to get started:

1. `LOGIN_URL` - this is the address of the webpage the login form SUBMITS to. We have the `/login` URL, but down below you can see this is not the URL we need.
2. `PASS_FILE` - the local path to a password file.
3. `RHOSTS` - the `target's` IP address.
4. `STOP_ON_SUCCESS` - once a correct username/password combo is found, we want to stop the tool. We just need one credential.
5. `USER_FILE` - the local filepath to a file of usernames.

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/3msfburp.png "/>

As mentioned earlier, the value of `LOGIN_URL` can be determined with a proxy. I went back to the Jenkins login page and turned on `FoxyProxy` to route the POST data to `Burpsuite`. After filling in dummy data in the username/password fields and submitting, the data appeared on the `Intercept` tab. We can see the `LOGIN_URL` value is in the top line of the POST data.

Note: if you are using `hydra`, you would need to notate `line 14` for the POST variables.

Time to set the values for the module options:

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/3msfsetoptions.png "/>

Once the options were set, I ran the package with `run`...

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/3msfsuccess.png "/>

...and had success within a few seconds lol

The working credential pair is `root:password`.

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/3msfunset.png "/>

Before going back, I `unset` all options to restore their values to defaul and quite `msfconsole` with `exit`.

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/4version.png "/>

I logged into the web portal with the working creds. Finally I retrieved the Jenkins version at the bottom of the dashboard: `2.289.1`

### Task 5
#### What type of script is accepted as input on the Jenkins Script Console?


<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/groovy.gif"/>

`Groovy` per the screenshot above.


### Task 6
#### What would the "String cmd" variable from the Groovy Script snippet be equal to if the Target VM was running Windows?

`cmd.exe`, the command prompt.

### Task 7
#### What is a different command than "ip a" we could use to display our network interfaces' information on Linux?

`ifconfig`

### Task 8
#### What switch should we use with netcat for it to use UDP transport mode?

`-u`

### Task 9
####  What is the term used to describe making a target host initiate a connection back to the attacker host?

`reverse shell`

## Capturing the Flag

From these tasks, we can gather that we need to create a reverse shell from the `target` to our localhost. This will be done by abusing the script editor inside of Jenkins.

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/4script.png"/>

**Abitrary code execution**. NOICE.

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/5scriptconsole.png"/>

A quick google search showed some pre-crafted payloads for Groovy Script:

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/osint.PNG"/>

The payload I chose can be found [here](https://gist.github.com/frohoff/fed1ffaab9b9beeb1c76)

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/6script.png"/>

The only edit needed was to replace `localhost` with my local machine's IP from the network interface that was on the same network as the VM, as well as noting the port the reverse shell would be calling to.


<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/7reverseshell.png"/>

Before running the script, I launched `netcat` to setup a listener for the reverse shell on my local host.

`netcat -lvnp 8000` - the port specified here has to match the port specific in the reverse shell script.

Once the local server was listening, I ran the Groovy script and got a reverse shell connection.

`whoami` shows that the Jenkin's script runs under `root` context. Big oof.

<img src="/assets/img/ctf/htb/sp/tier1/pennyworth/flag.png"/>

From there I went to `root`'s home and `cat`ted the flag to pwn Pennyworth.

