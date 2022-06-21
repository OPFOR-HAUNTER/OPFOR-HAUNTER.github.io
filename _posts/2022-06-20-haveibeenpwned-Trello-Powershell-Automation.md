---
layout: post
title: "Automating haveibeenpwned Breach Searches with Powershell"
date: 2022-06-20
categories: BlueOps Detection
tags: BlueOps detection automation powershell haveibeenpwned trello daemon api
---
## Introduction
In an effort to automate as much as possible for my organization, I created two Powershell modules to help out our team with various tasks. This use case is the automation of checking [haveibeenpwned (HIBP)](https://haveibeenpwned.com) daily and confirming if any of our enterprise users were found in a breach. The daemon scripts also creates a Trello card with breach info and affected users.

### tl;dr                                      
<details>                                                                                      
  <summary>Spoiler!</summary>                                                                  
   1. Enterprise users sometimes register with 3rd parties with their work email. With the possibility of the reuse of passwords with their 3rd party accounts, we track users found in breaches on haveibeenpwned.<br/>
   2. HIBP Powershell module contains functions for automated haveibeenpwned processes for an enterprise.<br/>
   3. Trello Powershell module contains functions for getting Trello infos and creating. Our org ingests alerts from various tools to Trello for uniform visibility and efficiency.<br/>          
   4. The HIBP Daily Breach Trello Daemon is a Powershell script usecase utilizing both modules.<br/>
   5. More advanced automations can be done with the HIBP module. E.g., emailing users, summary reports, disabling user accounts (not included in this repo).<br/>
   6. I am NOT a Powershell guru...and the code reflects this :S                                     
</details>      

## Required Resources
* [haveibeenpwned API Powershell Module](https://github.com/OPFOR-HAUNTER/SecOps/blob/main/BlueOps/Detection/HIBP/HIBP.psm1)
* [Trello API Powershell Module](https://github.com/OPFOR-HAUNTER/SecOps/blob/main/NullOps/Automation/Trello.psm1)
* [HIBP Daily Breach Trello Daemon](https://github.com/OPFOR-HAUNTER/SecOps/blob/main/BlueOps/Detection/HIBP/HIBP_Daily_Breach_Trello_Daemon_Example.ps1)
* [HIBP API (v3)](https://haveibeenpwned.com/API/v3) - API Key Required @ $3.50/month

## The Problem(s)
### Cumbersome, Reactive, Manual Process 

Lack of visibility and a unified threat alert platform for a multitude of security tools can lead to gaps in response time and monitoring efficiency. Currently, HIBP notifies organization via an email. Depending on many factors, this can delay the response to investigating the breach for affected users.

<figure><img src='/assets/img/BlueOps/Detection/HIBP/HIBP_Notification_email.PNG'/><figcaption>An example HIBP notification email.</figcaption>
</figure>


At the time of authoring these scripts, the HIBP API did not have the capability of pulling an enterprise-wide call of all users found in a given breach. Instead, a SOC member would have to manually visit HIBP, enter our organization email, wait for the resulting CSV, filter the returned list by the most recent breach, and then finally verify each user. This verification part was partically cumbersome for larger breaches that may contain dozens or even hundreds of our users. 

<figure><img src='/assets/img/BlueOps/Detection/HIBP/HIBP_Notification_email2.PNG'/><figcaption>Note that visiting the HIBP website is required to determine which accounts were expired.</figcaption>
</figure>

HIBP reports all email addresses for a given enterprise in ALL existing breaches. This requires SOC staff to manually filter a CSV for the most recent breach that was reported. Additionally, as some of these breaches may have occurred years ago many users reported could be disabled, resulting in inefficient processing time.

<figure><img src='/assets/img/BlueOps/Detection/HIBP/HIBP_CSV_Example.PNG'/><figcaption>An example CSV that is returned from a GUI domain search. ALL breaches are returned for every user in your domain.</figcaption>
</figure>

## The Solution

I created an automated daemon that runs daily. This allows us to proactively search for a breach posted on HIBP, parse enabled users against the breach and verify those affected, and then create a Trello card with info. 

<figure><img src='/assets/img/BlueOps/Detection/HIBP/Trello_Cards.PNG'/><figcaption>Populated Trello cards. Note that the last card had a second label (blue) applied due to a high-risk factor we defined for breaches (below).</figcaption>
</figure>

There are three attributes to a breach that our SOC checks for high risk factors that require an escalated response:<br/> 
	* BreachDate - the date it was published on the darkweb. <br/>
	* AddedDate - the date the breach was posted on haveibeenpwned.com.<br/>
	* DataClasses - These are the types of data the breach contained. E.g., Email addresses, Credit card info, & passwords. We classify breaches with Passwords as high risk.

<figure><img src='/assets/img/BlueOps/Detection/HIBP/Trello_Card.PNG'/><figcaption>A generated card. Breach data, label, affected users are populated. User's SamAccountNames and PasswordLastSet are included in the details.</figcaption> 
</figure>

## Final Thoughts

These scripts are written terribly and can be refactored by someone more talented. The time saved is a plus, and it was a great learning experience. Before our on-prem SMTP server was decommissioned there was an additional function to email affected users, and optionally disable accounts based on additional risk factors found in the breach. Maybe one day I'll get back to adding them...

