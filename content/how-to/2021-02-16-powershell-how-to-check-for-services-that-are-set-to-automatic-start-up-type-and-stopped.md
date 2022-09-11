---
title: Powershell – How to check for services that are set to ‘Automatic’ start up type and ‘Stopped’
author: Daniel Hayes
type: post
date: 2021-02-16T17:21:40+00:00
categories:
  - How-Tos
tags:
  - automatic
  - how
  - how-to
  - one-liner
  - powershell
  - startup
  - state
  - stopped
  - type

---
Powershell is a really powerful tool and can be used to automate tasks during troubleshooting. 

One of the issues that I have seen in the past is that services will not start automatically after an update. Depending on the amount of services on a machine it can be a time consuming process to check for automatic services that are not started. 

With Powershell we can determine what services are set to automatic and aren&#8217;t started with a simple little one liner. 

<div class="wp-block-syntaxhighlighter-code ">
  <pre class="brush: powershell; title: ; notranslate" title="">
Get-Service | Select-Object -Property Name,Status,StartType | Where-Object {$_.Status -eq "Stopped" -and $_.StartType -eq "Automatic"}
</pre>
</div>

It should return a result similar to the one below:<figure class="wp-block-image size-large">

<img loading="lazy" width="834" height="167" src="https://danielhayes.tech/wp-content/uploads/2021/02/image.png" alt="" class="wp-image-99" srcset="https://danielhayes.tech/wp-content/uploads/2021/02/image.png 834w, https://danielhayes.tech/wp-content/uploads/2021/02/image-300x60.png 300w, https://danielhayes.tech/wp-content/uploads/2021/02/image-768x154.png 768w" sizes="(max-width: 834px) 100vw, 834px" /> </figure> 

Now with this simple one liner you are able to see what services are not started.