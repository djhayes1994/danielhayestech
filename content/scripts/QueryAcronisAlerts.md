---
title: Powershell – Querying the Acronis Alerts API
author: Daniel Hayes
type: post
date: 2021-10-29T17:55:42+00:00
url: /2021/10/29/powershell-querying-the-acronis-alerts-api/
featured_image: /wp-content/uploads/2020/09/powershell-logo-2.gif
categories:
  - Scripts
tags:
  - Acronis
  - alerts
  - API
  - cyber
  - power
  - powershell
  - protect
  - shell

---
 

Recently I was trying to find a way to query the Acronis alerts API so that I could review errors quickly. 

Previously these were being reviewed manually via the management dashboard. 

I started out by reviewing some of the example code available on the Acronis github repos.  
<https://github.com/acronis/acronis-cyber-platform-powershell-examples>

After reviewing the code I started writing my own script. This script will go through and find the following:

  1. Jobs that have failed with the &#8216;BackupFailed&#8217; type.
  2. Jobs that have failed with the &#8216;BackupDidNotStart&#8217; type.
  3. Offline agents.

After it returns those machines it will create two csv files in the C:\temp directory. This directory can be changed in the following variables:

$outfileFailed

$outfileOffline

For this code to work you will need to generate the clientID and clientSecret via the Acronis console. 

You can find an example of the code below and on <a href="https://github.com/djhayes1994/Powershell/blob/master/Acronis-GetFailedBackups.ps1" data-type="URL" data-id="https://github.com/djhayes1994/Powershell/blob/master/Acronis-GetFailedBackups.ps1" target="_blank" rel="noreferrer noopener">GitHub</a>.  
  


```powershell
$clientId = "(REPLACE ME)"
$clientSecret = "(REPLACE ME)"

# Manually construct Basic Authentication Header
$pair = "${clientId}:${clientSecret}"
$bytes = [System.Text.Encoding]::ASCII.GetBytes($pair)
$base64 = [System.Convert]::ToBase64String($bytes)
$basicAuthValue = "Basic $base64"
$headers = @{ "Authorization" = $basicAuthValue }
# Use param to tell type of credentials we request
$postParams = @{ grant_type = "client_credentials" }

# Add the request content type to the headers
$headers.Add("Content-Type", "application/x-www-form-urlencoded")

$token = Invoke-RestMethod -Method Post -Uri "https://us-cloud.acronis.com/api/2/idp/token" -Headers $headers -Body $postParams

#Specifies what the header array can hold, in this case string and string.
$headers = New-Object "System.Collections.Generic.Dictionary[[String],[String]]"
#Adds auth info to header variable.
$bearerVal = $token.access_token
$headers.Add("Authorization", "Bearer $bearerVal")
$baseuri = "https://us-cloud.acronis.com/"
$endpoint = "api/alert_manager/v1/alerts"
$fullurl = $baseuri+$endpoint
#Sends a GET request to the Acronis API.
$response = Invoke-RestMethod $fullurl -Method 'GET' -Headers $headers

#Takes the items property from the JSON response. 
$retdata = ($response).items

# Creates new CSV files so that alerts can be appended to them.
# There are two seperate CSV files at this time, one for the Failures and one for the offline machines.
# CSV files are stored in the temp folder at this time. 
$outfileFailed = "C:\temp\alertsFailed.csv"
$newcsvFailed = {} | Select "resourcename","planname","errortext", "errormessagereason", "alertreceived" | Export-Csv $outfileFailed
$csvfileFailed = Import-CSV $outfileFailed

$outfileOffline = "C:\temp\alertsOfflineMachine.csv"
$newcsvOffline = {} | Select "resourcename","dayspassed" | Export-Csv $outfileOffline
$csvfileOffline = Import-CSV $outfileOffline

ForEach($id in $retdata){
    if($id.type -like "BackupFailed"){
        $resourceName = $id.details.resourceName
        $planName = $id.details.planName
        $errorText = $id.details.error.text
        $errorMessageReason = $id.details.errorMessage.reason
        $alertRec = $id.createdAt
        $alertUp = $id.updatedAt
        Write-Output "Name: $resourceName"
        Write-Output "Plan: $planName"
        Write-Output "Error: $errorText"
        Write-Output "Error Reason: $errorMessageReason"
        Write-Output "Alert Received: $alertRec"
        Write-Output "Alert Last Updated: $alertUp"
        $csvfileFailed.resourcename = $resourceName
        $csvfileFailed.planname = $planName
        $csvfileFailed.errortext = $errorText
        $csvfileFailed.errorMessageReason = $errorMessageReason
        $csvfileFailed.alertreceived = $alertRec
        $csvfileFailed | Export-Csv $outfileFailed -Append
        "`n"
    }

    if($id.type -like "BackupDidNotStart"){
        $resourceName = $id.details.resourceName
        Write-Output "Name: $resourceName"
        Write-Output "Error: Backup did not start."
        $csvfileFailed.resourcename = $resourceName
        $csvfileFailed.planname = $null
        $csvfileFailed.errortext = "Backup did not start"
        $csvfileFailed.errorMessageReason = $null
        $csvfileFailed.alertreceived = $alertRec
        $csvfileFailed | Export-Csv $outfileFailed -Append
        "`n"
    }
    
    if($id.type -like "MachineOffline*"){
        $resourceName = $id.details.resourceName
        $alertRec = $id.createdAt
        $alertUp = $id.updatedAt
        $daysPassed = $id.details.daysPassed
        Write-Output "Name: $resourceName"
        Write-Output "Days Since Last Check-In: $daysPassed"
        Write-Output "Alert Received: $alertRec"
        Write-Output "Alert Last Updated: $alertUp"
        $csvfileOffline.resourcename = $resourceName
        $csvfileOffline.dayspassed = $daysPassed
        $csvfileOffline | Export-Csv $outfileOffline -Append
        "`n"
    }
}
```