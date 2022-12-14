---
title: Powershell – Meraki VPN Configuration Script
author: Daniel Hayes
type: post
date: 2021-02-17T13:27:02+00:00
categories:
  - Scripts
tags:
  - client
  - client-vpn
  - configuration
  - Meraki
  - powershell
  - vpn

---
This script will configure a Windows LT2P vpn connection based on the input provided. 

Setup of the VPN is based off of information found in the Meraki KB article:  
<a rel="noreferrer noopener" href="https://documentation.meraki.com/MX/Client_VPN/Client_VPN_OS_Configuration" target="_blank">https://documentation.meraki.com/MX/Client_VPN/Client_VPN_OS_Configuration </a>

Github: <a rel="noreferrer noopener" href="https://github.com/djhayes1994/Powershell/blob/master/MerakiVPNConfiguration.ps1" target="_blank">https://github.com/djhayes1994/Powershell/blob/master/MerakiVPNConfiguration.ps1</a>

```powershell
<#
.SYNOPSIS
  The purpose of this script is to minimize the ammount of work required to create a VPN connection on a Windows 8, 8.1, or 10 workstation for Meraki VPN.
.DESCRIPTION
  Collects input from shell and inputs it into Add-VPNConnection command with the command structured for Meraki L2TP VPN connections.
.INPUTS
  Name - This is the name of the VPN connection that will show within the Windows UI.
  ServerAddr - This is the server address which can be found either via the Meraki Dashboard or via CWM configurations, typically the configuration is named Remote Access.
  L2TPPSK - This is the preshared key for the L2TP connection. This can be found either via the Meraki Dashboard or via the customers configurations.
  DnsSuffix - This is the dns suffix used by the VPN connection, for example: contoso.local
.OUTPUTS
  Add-VPNConnection creates the VPN connection. 
.NOTES
  Version:        1.2
  Author:         Daniel Hayes
  Creation Date:  03/28/2019
  Updated: 02/07/2021
  Purpose/Change: Added DNSsuffix variable and added DNS suffix switch to Add-VPNConnection command. 
  
.EXAMPLE
  End user is requesting VPN access and the customer utilizes Meraki VPN. Meraki VPN does not have a client so it uses the Windows native VPN client. 
#>

#----------------------------------------------------------[Declarations]----------------------------------------------------------

$Name = Read-Host -Prompt 'Input name of VPN connection; Ie. Company VPN'
$ServerAddr = Read-Host -Prompt 'Input server address can be WAN IP or Meraki Hostname'
$L2TPPSK = Read-Host -Prompt 'Input Pre-shared key for VPN, can be found in Remote Access configuration'
$DnsSuffix = Read-Host -Prompt 'Input the dns suffix used for the VPN connection'

#-----------------------------------------------------------[Execution]------------------------------------------------------------
Import-Module VpnClient
Add-VpnConnection -RememberCredential -Name $Name -ServerAddress $ServerAddr -AuthenticationMethod Pap -TunnelType L2tp -EncryptionLevel Optional -L2tpPsk $L2TPPSK -DnsSuffix $DnsSuffix -Force
Write-Host "VPN Connection has been created..."
Write-Host "VPN Display Name:" $Name
Write-Host "Server:" $ServerAddr
Write-Host "Pre-Shared key:" $L2TPPSK "was used."
Write-Host "Detailed information is located below...."
Get-VpnConnection | fl
Pause
```