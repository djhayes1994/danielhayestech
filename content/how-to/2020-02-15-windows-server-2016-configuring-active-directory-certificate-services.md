---
title: Windows Server 2016 – Configuring Active Directory Certificate Services
author: Daniel Hayes
type: post
date: 2020-02-15T15:58:13+00:00
categories:
  - How-Tos
tags:
  - 2016
  - active
  - ad
  - certificate
  - configuration
  - configure
  - configuring
  - cs
  - directory
  - ldap
  - ldaps
  - server
  - services
  - ssl
  - windows

---
  1. Log into your server that you are installing the role on, or a server that has the ability to manage the destination server.
  2. Open the server manager application. (servermanager.exe)
  3. Click ‘Manage > Add Roles and Features’  
<img loading="lazy" width="1513" height="1058" class="wp-image-43" src="https://danielhayes.tech/wp-content/uploads/2020/02/1.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/1.png 1513w, https://danielhayes.tech/wp-content/uploads/2020/02/1-300x210.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/1-1024x716.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/1-768x537.png 768w" sizes="(max-width: 1513px) 100vw, 1513px" /> 
  4. The ‘Add Roles and Features Wizard’ will now open, in the ‘Before You Begin’ page click the ‘Next’ button.  
<img loading="lazy" width="1181" height="844" class="wp-image-44" src="https://danielhayes.tech/wp-content/uploads/2020/02/2.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/2.png 1181w, https://danielhayes.tech/wp-content/uploads/2020/02/2-300x214.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/2-1024x732.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/2-768x549.png 768w" sizes="(max-width: 1181px) 100vw, 1181px" /> 
  5. In the ‘Installation Type’ page choose ‘Role-based or feature-based installation’.
  6. Click ‘Next’  
<img loading="lazy" width="1182" height="846" class="wp-image-45" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/3.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/3.png 1182w, https://danielhayes.tech/wp-content/uploads/2020/02/3-300x215.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/3-1024x733.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/3-768x550.png 768w" sizes="(max-width: 1182px) 100vw, 1182px" /> 
  7. In the server selection screen keep the current settings and hit ‘Next >’.
      * If you are using another server to install the role on the target server choose the correct server.
  8. Click ‘Next >  
<img loading="lazy" width="1181" height="848" class="wp-image-46" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/4.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/4.png 1181w, https://danielhayes.tech/wp-content/uploads/2020/02/4-300x215.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/4-1024x735.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/4-768x551.png 768w" sizes="(max-width: 1181px) 100vw, 1181px" /> 
  9. On the ‘Server Roles’ page choose the role ‘Active Directory Certificate Services’.  
<img loading="lazy" width="333" height="36" class="wp-image-47" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/5.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/5.png 333w, https://danielhayes.tech/wp-content/uploads/2020/02/5-300x32.png 300w" sizes="(max-width: 333px) 100vw, 333px" /> 
 10. A new window will pop up confirming the roles and features that need added. Keep the defaults and click the ‘Add Features’ button.  
<img loading="lazy" width="625" height="652" class="wp-image-48" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/6.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/6.png 625w, https://danielhayes.tech/wp-content/uploads/2020/02/6-288x300.png 288w" sizes="(max-width: 625px) 100vw, 625px" /> 
 11. In the ‘Features’ page click ‘Next >’.
 12. In the ‘Active Directory Certificate Services’ page click ‘Next >’.
 13. &nbsp;In the ‘Role Services’ page leave the defaults and click ‘Next >’.
 14. In the confirmation page leave the ‘Restart the destination server automatically if required’ unchecked. Click ‘Install’.  
<img loading="lazy" width="1178" height="846" class="wp-image-50" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/8.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/8.png 1178w, https://danielhayes.tech/wp-content/uploads/2020/02/8-300x215.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/8-1024x735.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/8-768x552.png 768w" sizes="(max-width: 1178px) 100vw, 1178px" /> 
 15. Allow the installation to complete.
 16. Once complete click the ‘Configure Active Directory Certificate Services on the destination server’ hyperlink.  
<img loading="lazy" width="1183" height="843" class="wp-image-54" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/9.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/9.png 1183w, https://danielhayes.tech/wp-content/uploads/2020/02/9-300x214.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/9-1024x730.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/9-768x547.png 768w" sizes="(max-width: 1183px) 100vw, 1183px" /> 
 17. After clicking the hyper link a new window will open named ‘AD CS Configuration’
 18. On the ‘Credentials’ page provide credentials, it will use the current logged in user by default.
 19. Click ‘Next >’.  
<img loading="lazy" width="1146" height="846" class="wp-image-55" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/10.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/10.png 1146w, https://danielhayes.tech/wp-content/uploads/2020/02/10-300x221.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/10-1024x756.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/10-768x567.png 768w" sizes="(max-width: 1146px) 100vw, 1146px" /> 
 20. In the setup type you will need to specify whether or not you want to install the CA as a Enterprise CA or a Standalone CA.
      * In this guide I am setting up a Standalone CA. 
      * If you are installing this CA in a Active Directory environment you will want to configure a Enterprise CA (Especially if you are performing these steps to set up LDAPS).
 21. Click ‘Next >’.  
<img loading="lazy" width="1148" height="843" class="wp-image-56" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/11.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/11.png 1148w, https://danielhayes.tech/wp-content/uploads/2020/02/11-300x220.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/11-1024x752.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/11-768x564.png 768w" sizes="(max-width: 1148px) 100vw, 1148px" /> 
 22. In the ‘CA Type’ window you will be prompted to choose Root CA or Subordinate CA.
      * Choose a Root CA if this server is going to be the primary certificate authority.
      * If you already have a Root CA in your environment and you are looking to add a second CA that is authorized to issue certificates from the Root CA then choose Subordinate CA.
 23. After choosing your ‘CA Type’ click ‘Next >’.  
<img loading="lazy" width="1146" height="846" class="wp-image-57" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/12.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/12.png 1146w, https://danielhayes.tech/wp-content/uploads/2020/02/12-300x221.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/12-1024x756.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/12-768x567.png 768w" sizes="(max-width: 1146px) 100vw, 1146px" /> 
 24. In the ‘Private Key’ page we are going to want to create a new private key. Choose ‘Create a new private key’. Then click ‘Next >’.  
<img loading="lazy" width="1145" height="844" class="wp-image-58" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/13.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/13.png 1145w, https://danielhayes.tech/wp-content/uploads/2020/02/13-300x221.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/13-1024x755.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/13-768x566.png 768w" sizes="(max-width: 1145px) 100vw, 1145px" /> 
 25. For the ‘Cryptography’ page choose the following options, unless your environment calls for other settings.
      * Cryptographic Provider: RSA#Microsoft Software Key Storage Provider
      * Key Length: 2048
      * Hashing Algorithm: SHA256
 26. Click ‘Next >’.  
<img loading="lazy" width="1145" height="844" class="wp-image-59" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/14.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/14.png 1145w, https://danielhayes.tech/wp-content/uploads/2020/02/14-300x221.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/14-1024x755.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/14-768x566.png 768w" sizes="(max-width: 1145px) 100vw, 1145px" /> 
 27. In the ‘CA Name’ set the common name for this CA to the machine’s hostname. 
 28. Click ‘Next >’.  
<img loading="lazy" width="1147" height="845" class="wp-image-60" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/15.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/15.png 1147w, https://danielhayes.tech/wp-content/uploads/2020/02/15-300x221.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/15-1024x754.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/15-768x566.png 768w" sizes="(max-width: 1147px) 100vw, 1147px" /> 
 29. For the validity period choose 5 years. Then click ‘Next >’.  
<img loading="lazy" width="1142" height="844" class="wp-image-61" style="width: px;" src="https://danielhayes.tech/wp-content/uploads/2020/02/16.png" alt="" srcset="https://danielhayes.tech/wp-content/uploads/2020/02/16.png 1142w, https://danielhayes.tech/wp-content/uploads/2020/02/16-300x222.png 300w, https://danielhayes.tech/wp-content/uploads/2020/02/16-1024x757.png 1024w, https://danielhayes.tech/wp-content/uploads/2020/02/16-768x568.png 768w" sizes="(max-width: 1142px) 100vw, 1142px" /> 
 30. In the ‘Certificate Database’ page leave the defaults and click ‘Next >’.
 31. In the ‘Results’ page click ‘Close’.
 32. If you set up the CA on a DC for use with LDAPS then you will want to reboot and then from a administrative command prompt run:

<div class="wp-block-syntaxhighlighter-code ">
  <pre class="brush: bash; title: ; notranslate" title="">
Gpupdate /force
</pre>
</div>