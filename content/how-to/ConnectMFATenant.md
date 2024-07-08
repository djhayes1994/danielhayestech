---
title: 'Powershell – How to connect to Exchange Online on a MFA  protected tenant.'
author: Daniel Hayes
type: draft
date: 2021-02-16T17:35:28+00:00
categories:
  - How-Tos
tags:
  - 365
  - Exchange
  - ExchangeOnlineManagement
  - how
  - how-to
  - Office
  - Office365
  - Online
  - powershell

---

# THIS PAGE IS UNDER CONSTRUCTION - I'M MISSING IMAGES/FORMATTING
With the introduction of the security baselines from Microsoft it is necessary for you to use Modern Authentication in your PowerShell scripts/if you want to connect to Exchange Online. 

Connecting to Exchange Online is a pretty easy process and you can do so by following the steps below:

  1. Open Powershell and install the Exchange Online module. To do this you will need to run the following command:

<div class="wp-block-syntaxhighlighter-code ">
  <pre class="brush: powershell; title: ; notranslate" title="">
Install-Module ExchangeOnlineManagement
</pre>
</div>

<ol start="2">
  <li>
    After the module has been installed you will want to import the module so the commands are available. To do this you will need to run the following command:
  </li>
</ol>

<div class="wp-block-syntaxhighlighter-code ">
  <pre class="brush: powershell; title: ; notranslate" title="">
Import-Module ExchangeOnlineManagement
</pre>
</div>

<ol start="3">
  <li>
    Once the module has been imported you will need to connect to Exchange Online.
  </li>
</ol>

<div class="wp-block-syntaxhighlighter-code ">
  <pre class="brush: powershell; title: ; notranslate" title="">
Connect-ExchangeOnline -UserPrincipalName &lt;your admin upn&gt;
</pre>
</div>

<ol start="4">
  <li>
    You will now be prompted for credentials. Provide the credentials and approve the MFA request via your MFA app (Duo, Authenticator, etc.)
  </li>
  <li>
    If it was successful you will receive a prompt like the one below:
  </li>
</ol><figure class="wp-block-image size-large">

<img loading="lazy" width="839" height="347" src="https://danielhayes.tech/wp-content/uploads/2021/02/image-1.png" alt="" class="wp-image-102" srcset="https://danielhayes.tech/wp-content/uploads/2021/02/image-1.png 839w, https://danielhayes.tech/wp-content/uploads/2021/02/image-1-300x124.png 300w, https://danielhayes.tech/wp-content/uploads/2021/02/image-1-768x318.png 768w" sizes="(max-width: 839px) 100vw, 839px" /> </figure> 

<ol start="6">
  <li>
    You can now run Exchange Online Powershell commands to administer your Exchange Online tenant.
  </li>
</ol>
