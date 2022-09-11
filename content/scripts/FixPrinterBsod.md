---
title: ConnectWise Automate – Deploy Out of Band Updates for Printing Issues
author: Daniel Hayes
type: post
date: 2021-03-24T13:57:57+00:00
categories:
  - Scripts
tags:
  - 1909
  - 20H2
  - automate
  - BSOD
  - connectwise
  - issues
  - KB5001648
  - KB5001649
  - patching
  - printing
  - script

---
 

Recently there were issues with the March CU updates that caused issues with printing.

I was having issues deploying the out of band patches via the Connectwise Automate patch manager, I have made a script to push these updates manually.

Script flow:

  1. Make sure the agent is running Windows.
  2. Make sure the agent is running Windows 10.
  3. Verify ReleaseID matches requrired versions for the KB article(s).
  4. Download the correct KB from the Microsoft Update Catalogue
  5. Install the update via the Windows Update Agent.
  6. Prompt the user to reboot (does not force the reboot)

You can find the script here: <a rel="noreferrer noopener" href="https://github.com/djhayes1994/Public-LT-Scripts/blob/master/Fix%20Printer%20BSOD%20CU%20Update.xml" target="_blank">https://github.com/djhayes1994/Public-LT-Scripts/blob/master/Fix%20Printer%20BSOD%20CU%20Update.xml</a>

To install the script just import the XML file into Automate. The script will be in a folder called rerelease.