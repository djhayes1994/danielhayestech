---
title: Connectwise Automate – Monitoring whether or not Liongard Agents are set to auto update.
author: Daniel Hayes
type: post
date: 2021-11-09T18:51:27+00:00
categories:
  - How-Tos
tags:
  - auto
  - automate
  - connectwise
  - how
  - how-to
  - liongard
  - monitor
  - powershell
  - remote
  - remote monitor
  - roar
  - script
  - to
  - update

---
I recently attended the product update webinar for Liongard. It was recommended that you check whether or not agents were set to auto update.

After a little bit of digging I found that there was a xml file in the Liongard directory that contained this info.

I wrote a small one liner with Powershell to create a Powershell object with the contents of the XML file and then return the value of it. 

```powershell
"%windir%\system32\WindowsPowerShell\v1.0\PowerShell.exe" -command "[xml]$xmlElm = Get-Content -Path 'C:\Program Files (x86)\LiongardInc\LiongardAgent\LiongardAgentUpdater.xml';$xmlElm.task.settings.enabled"
```

Using this code you can create a remote monitor in Automate with the following settings:

![Script Screenshot](/Liongard.png)

This monitor will check every 5 minutes to make sure that the value is set to &#8216;True&#8217;. If it is set to false then the monitor will fail.

I won&#8217;t be going over how to do this in this post, however you could easily create an advanced search for machines with the Liongard Agent installed and have it run against those machines&#8230;if you wanted to get really fancy you could create a auto remediation script that will change the value to &#8216;True&#8217; and/or update the agent via the LiongardAgentUpdater.exe found in the same directory as the XML file.