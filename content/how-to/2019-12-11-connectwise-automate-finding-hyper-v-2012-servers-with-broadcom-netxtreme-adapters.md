---
title: ConnectWise Automate – Finding Hyper-V 2012 servers with Broadcom NetXtreme Adapters
author: Daniel Hayes
type: post
date: 2019-12-11T21:11:35+00:00
categories:
  - How-Tos
tags:
  - adapter
  - automate
  - broadcom
  - connectivity
  - connectwise
  - how
  - how-to
  - hyper
  - hyper-v
  - loss
  - mysql
  - netxtreme
  - to
  - v

---
There is a reported issue with Hyper-V servers running Microsoft Server 2012 and Microsoft Server 2012 R2 where BroadCom NetExtreme adapters with VMQ enabled will have VMs lose connectivity intermittently.  
  
Information on the issue can be found here: <https://support.microsoft.com/en-us/help/2986895/virtual-machines-lose-network-connectivity-when-you-use-broadcom-netxt>

You can utilize SQLYog to run the query below on a on premise ConnectWise Automate installation. 

<div class="wp-block-syntaxhighlighter-code ">
  <pre class="brush: sql; title: ; notranslate" title="">
SELECT
	computers.computerid AS 'Computer Id',
	computers.name AS 'Computer Name',
	clients.name AS 'Client Name',
	inv_networkcard.Description AS 'Network Card',
	computers.os AS 'OS Type',
	computerroledefinitions.RoleDefinitionID AS 'Role ID',
	roledefinitions.RoleName AS 'Role Name'
FROM Computers
LEFT JOIN Clients ON (Computers.ClientId=Clients.ClientId)
LEFT JOIN inv_networkcard ON (inv_networkcard.ComputerID=Computers.ComputerID)
LEFT JOIN computerroledefinitions ON (computerroledefinitions.ComputerID=Computers.ComputerID)
LEFT JOIN roledefinitions ON (roledefinitions.RoleDefinitionID=computerroledefinitions.RoleDefinitionID)
WHERE inv_networkcard.Description LIKE '%Broadcom%NetXtreme%' AND computers.os LIKE '%server%2012%' AND roledefinitions.RoleName LIKE '%Hyper-v%';
</pre>
</div>

This MySQL query will return all Windows Server 2012 devices with the Hyper-V role that have Broadcom NetXtreme adapters. This will help identify possible issues before they arise.