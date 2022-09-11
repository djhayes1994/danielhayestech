---
title: Powershell – Update Meraki Org IDP Fingerprints
author: Daniel Hayes
type: post
date: 2022-04-06T22:20:18+00:00
categories:
  - Scripts
tags:
  - API
  - fingerprint
  - idp
  - Meraki
  - powershell
  - saml
  - sha1

---
The certificates used for Meraki SAML configuration expire after a certain period of time.

Because of the way Meraki handles this, you have to set the fingerprint on the child organizations (see: <a rel="noreferrer noopener" href="https://documentation.meraki.com/General_Administration/Managing_Dashboard_Access/Configuring_SAML_SSO_with_Azure_AD" target="_blank">https://documentation.meraki.com/General_Administration/Managing_Dashboard_Access/Configuring_SAML_SSO_with_Azure_AD</a>)

Basically what this means is that when it comes time to renew the cert you have to update the SHA1 fingerprint on your parent org and child organizations. 

This can be a very time consuming process if done manually. 

I have written a script that will take care of most of the work.



**What the script does:**  
The script will query the organizations API endpoint to get a list of all of your Meraki Orgs.

After all of the orgs are returned it will check to see if the API is enabled for each org, if it is enabled then it will query the /saml/idps/ API endpoint to get a list of IDPs for each organization.

After it has the IDPs for each organization it will attempt to do a PUT request to the idpID that has the $previousFingerPrint value. This PUT request will update the x509certSha1Fingerprint for the corresponding idpID. 



Please make sure that you read the instructions below the Github link in their entirety. Failure to do so may result in you locking yourself out (if SAML is your only means of authentication).



Github: <a href="https://github.com/djhayes1994/Powershell/blob/master/MerakiOrgSamlIDP.ps1" target="_blank" rel="noreferrer noopener">https://github.com/djhayes1994/Powershell/blob/master/MerakiOrgSamlIDP.ps1</a>



**Instructions:**

  1. Download or copy the contents of the .ps1 file.
  2. Modify the variable $apikey to use your API key.
  3. Modify the variable $previousFingerPrint to the value of your current SHA1 fingerprint.
  4. Modify the variable $newFingerPrint to the value of your newly created SHA1 fingerprint.  
    **NOTE: Make sure that your fingerprints are formatted corrrectly!**  
    Example: 13:8F:K3:KF:32:F3:2F:WE:GT:43:A3:2S:54:4G:3Q:Y4:3V:HA:03:5G
  5. Run the script. 
  6. Log into the Meraki dashboard with a non SAML authenticated account.
  7. Grab the new value for the SAML Assertion Consumer Service URL from your tenant.
  8. Update your SAML provider.