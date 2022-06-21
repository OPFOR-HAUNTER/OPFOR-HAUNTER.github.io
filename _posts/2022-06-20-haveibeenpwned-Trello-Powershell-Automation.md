---
layout: post
title: "Automating haveibeenpwned Breach Searches with Powershell"
date: 2022-06-20
categories: BlueOps Detection
tags: BlueOps detection automation powershell haveibeenpwned trello 
---
<img src='/assets/img/ctf/htb/sp/tier2/.PNG'/>

## Introduction
In an effort to automate as much as possible for my organization, I created two Powershell modules to help out our team with various tasks. This use case is the automation of checking [haveibeenpwned (HIBP)](https://haveibeenpwned.com) daily and confirming if any of our enterprise users were found in a breach. 

At the time of authoring these scripts, the HIBP API did not have the capability of pulling an enterprise-wide call of all users found in a given breach. Instead, a SOC member would have to manually visit HIBP, enter our organization email, wait for the resulting CSV, filter the returned list by the most recent breach, and then finally verify each user. This verification part was partically cumbersome for larger breaches that may contain dozens or even hundreds of our users. 

Firstly, HIBP reports all email addresses for a given enterprise in a given breach. However, as some of these breaches may have occurred years ago, many users reported could be disabled.

Secondly, there are three attributes to a breach that our SOC considers high risk factors that require an escalated response. 
	* BreachDate - the date it was published on the darkweb. 
	* AddedDate - the date the breach was posted on haveibeenpwned.com.
	* DataClasses - These are the types of data the breach contained. E.g., Email addresses, Credit card info, & passwords.



### Code
* [haveibeenpwned API Powershell Module](https://github.com/OPFOR-HAUNTER/SecOps/blob/main/BlueOps/Detection/HIBP/HIBP.psm1)
* [Trello API Powershell Module](https://github.com/OPFOR-HAUNTER/SecOps/blob/main/NullOps/Automation/Trello.psm1)
* [HIBP Daily Breach Trello Daemon](https://github.com/OPFOR-HAUNTER/SecOps/blob/main/BlueOps/Detection/HIBP/HIBP_Daily_Breach_Trello_Daemon_Example.ps1)
* [HIBP API (v3)](https://haveibeenpwned.com/API/v3)

### tl;dr                                      
<details>                                                                                      
  <summary>Spoiler!</summary>                                                                  
                                                                                               
   1. <br/>
   2. <br/>          
   3. <br/>
   4. <br/>
   5. <figure><img src='/assets/img/ctf/htb/sp/tier2/.gif'/> <figcaption></figcaption></figure>                                     
</details>      


## Establishing a Connection & Initial Scan

Spawn the bastard and get vpn going.

I've confirmed the target is reachable with a `ping`.


## The Tasklist

### Task 1
####

### Task 2
####

### Task 3
####

### Task 4 
####

### Task 5
####

### Task 6
#### 

### Task 7
####

### Task 8
####

### Task 9
####  Submit root flag

## Capturing the Flag

<figure><img src='/assets/img/ctf/htb/sp/tier2/.gif'/> <figcaption></figcaption></figure>                                     

