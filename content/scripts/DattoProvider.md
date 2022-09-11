---
title: ConnectWise Automate – DattoProvider DLL Registration
author: Daniel Hayes
type: post
date: 2019-12-11T18:26:00+00:00
categories:
  - Scripts
tags:
  - automate
  - bug
  - connectwise
  - datto
  - dattoprovider
  - dll
  - fix
  - register
  - registration

---
There is an issue on the Datto Agent for Windows where the DattoProvider service will disappear, this script will fix the issue by re-registering the DLL.  
  
This also has a built in function for checking to make sure that the issue described above is actually happening. If the service is detected at the time the script is ran it will exit the script.  
  
This script makes use of PowerShell to verify if the issue exists and if the issue is resolved.  
  
The script can be found at: <https://github.com/djhayes1994/Public-LT-Scripts/blob/master/DattoProvider%20Registration.xml>

To install this script just import the xml file into ConnectWise Automate, the script will be under the script folder named Rerelease.

![Script Screenshot](/DattoProviderScript.png)