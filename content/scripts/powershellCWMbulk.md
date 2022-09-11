---
title: Powershell – Using the ConnectWise Manage API to modify configuration statuses
author: Daniel Hayes
type: post
date: 2020-09-28T19:32:28+00:00
categories:
  - Scripts
tags:
  - API
  - automate
  - chris
  - config
  - configuration
  - configurations
  - connectwise
  - cwa
  - cwm
  - manage
  - powershell
  - taylor

---
 

Recently I ran into an issue where assets synced from Connectwise Automate were not retired in Manage when they were retired in Automate.  
  
It turns out that the sync broke, it had since been fixed however I came to find that assets that were retired while the sync was broken were not updated when it was synced again. This resulted in a lot of stale information in the Connectwise Manage configurations.  
  
After having a chat session with Connectwise support I was told that there was no way to fix this without going in and touching each configuration.  
  
This lead me down a rabbit hole, which eventually lead to scoping out the issue by exporting our computers table from Automate and then checking the configurations for configurations that contained a DeviceID field that did not match up with a ComputerID in Connectwise Automate.  
  
I wanted to find an easy way to update the statuses of the old configurations, which lead me into trying to learn how to modify the configurations in Manage with API calls. This was unsuccessful, however I found a working Powershell module that did the API calls for me. Which can be found here: <a href="https://github.com/christaylorcodes/ConnectWiseManageAPI" data-type="URL" data-id="https://github.com/christaylorcodes/ConnectWiseManageAPI">https://github.com/christaylorcodes/ConnectWiseManageAPI</a>  
  
This lead to me messing around with the module and I eventually figured out how to change the statuses on configs in bulk. I wanted to share my code just in case someone else comes across a similar issue where they need to edit configuration statuses in bulk.  
  
I&#8217;ve added the code below, you can also find it <a href="https://github.com/djhayes1994/Powershell/blob/master/ChangeBulkConfigsCWM.ps1" data-type="URL" data-id="https://github.com/djhayes1994/Powershell/blob/master/ChangeBulkConfigsCWM.ps1">HERE</a> on GitHub. 

```powershell
<#
    Author: Daniel Hayes
    Version: 1.0
    Description: This script will pull a list of configurations from a .csv file and will update the configuration status.

    Changelog:
    
    1.0
    Created initial script. 
#>


<#
    This portion of the script will connect to the CWM instance via the CWM REST API.
#>


# We are declaring the connection info here for the CW instance. This stores as a hash table and the Connect-CWM function uses it to connect. 
$CWMConnectionInfo = @{
    # This is the URL to your manage server.
    Server      = 'yourcwserver.com'
    # This is the company entered at login
    Company     = 'CW Company'
    # Public key created for this integration
    pubkey      = 'Put your public key here'
    # Private key created for this integration
    privatekey  = 'Put your private key here'
    # ClientID found at https://developer.connectwise.com/ClientID
    clientid    = 'Your client ID here'
}
# ^This information is sensitive, take precautions to secure it.^

# Install/Update/Load the module
if(Get-InstalledModule 'ConnectWiseManageAPI' -ErrorAction SilentlyContinue) { Update-Module 'ConnectWiseManageAPI' -Verbose }
else { Install-Module 'ConnectWiseManageAPI' -Verbose }
Import-Module 'ConnectWiseManageAPI'

# Connect to your Manage server
Connect-CWM @CWMConnectionInfo -Force -Verbose

<#
    This is the body of the script and it's what makes the magic happen.

    We are importing a CSV file, path is defined by the ConfigPath variable.

    The configurations variable is what stores the info in a hash table. 

    For testing purposes the following IDs were set to 'Active'

    46914
    9199
    9200
    9174

    CSV should be formatted as:
    ID,
    46914,
    9199,
    9200,
    9174,

#>
$ConfigPath = "C:\Temp\ID.csv" 
$Configurations = Import-Csv -Path $ConfigPath
$LogPath = "C:\Temp\ConfigUpdateLog.txt"

#Enable logging to file specified in variable LogPath
Start-Transcript -Path $LogPath

#For each configuration ID listed in the CSV file we are going to change the status to 'Automate Inactive'.
ForEach ($config in $configurations){
    Update-CWMCompanyConfiguration -ID $config.ID -Operation replace -Path status/id -Value 7
}

#Stop logging because we don't care anymore. 
Stop-Transcript
```

Inside of the Update-CWMCompanyConfiguration you have to specify a -Value parameter, you will need to find the status ID that is used by your configurations and use that in place of &#8216;7&#8217;