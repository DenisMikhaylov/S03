```
Lab: Implementing an AD RMS infrastructure
Exercise 1: Installing and configuring AD RMS
 Task 1: Configure DNS and the AD RMS service account
1. Sign in to LON-DC1 as Adatum\Administrator by using the password Pa55w.rd.
2. In Server Manager, click Tools, and then click Active Directory Administrative Center.
3. Select and then right-click Adatum (local), click New, and then click Organizational Unit.
4. In the Create Organizational Unit dialog box, in the Name box, type Service Accounts, and then
click OK.
5. Right-click the Service Accounts organizational unit (OU) in the middle pane, click New, and then
click User.
6. In the Create User dialog box, provide the following details, and then click OK:
o First name: ADRMSSVC
o User UPN logon: ADRMSSVC
o User SamAccountName logon: Adatum\ADRMSSVC
o Password: Pa55w.rd
o Confirm Password: Pa55w.rd
o Password never expires: Enabled (you should click on Other password options to be able to
select this)
o User cannot change password: Enabled
7. Right-click the Users container, click New, and then click Group.
8. In the Create Group dialog box, type the following details, and then click OK:
o Group name: ADRMS_SuperUsers
o E-mail: ADRMS_SuperUsers@adatum.com
9. Right-click the Users container, click New, and then click Group.
10. In the Create Group dialog box, type the following details, and then click OK:
o Group name: Executives
o E-mail: executives@adatum.com
11. Double-click the Managers OU, and then Ctrl+click the following users:
o Aidan Norman
o Holly Spencer
12. In the Tasks pane, click Add to group.
13. In the Select Groups dialog box, type Executives, and then click OK.
14. Close the Active Directory Administrative Center.
15. In Server Manager, click Tools, and then click DNS.MCT USE ONLY. STUDENT USE PROHIBITED
L11-90 Implementing and administering AD RMS
16. In the DNS Manager console, click and expand LON-DC1, and then expand Forward Lookup Zones.
17. Select and then right-click Adatum.com, and then click New Host (A or AAAA).
18. In the New Host dialog box, type the following information, and then click Add Host:
o Name: adrms
o IP address: 172.16.0.21
19. Click OK, and then click Done.
Note: This is the address of LON-SVR1, where you will install AD RMS.
20. Close the DNS Manager console.
 Task 2: Install and configure the AD RMS server role
1. Sign in to LON-SVR1 as Adatum\Administrator by using the password Pa55w.rd.
2. Click Start, click Server Manager, click Manage, and then click Add Roles and Features.
3. In the Add Roles and Features Wizard, click Next three times.
4. On the Select server roles page, click Active Directory Rights Management Services.
5. In the Add Roles and Features Wizard dialog box, click Add Features, click Next four times, click
Install, and then, when the installation completes, click Close.
6. In Server Manager, click the AD RMS node.
7. Next to Configuration required for Active Directory Rights Management Services at LON-SVR1,
click More.
8. On the All Servers Task Details and Notifications page, click Perform additional configuration.
9. On the AD RMS page, in the AD RMS Configuration: LON-SVR1.adatum.com window, click Next.
10. On the AD RMS Cluster page, click Create a new AD RMS root cluster, and then click Next.
11. On the Configuration Database page, click Use Windows Internal Database on this server, and
then click Next.
12. On the Service Account page, click Specify.
13. In the Windows Security dialog box, type the following details, click OK, and then click Next:
o User name: ADRMSSVC
o Password: Pa55w.rd
14. On the Cryptographic Mode page, click Cryptographic Mode 2, and then click Next.
15. On the Cluster Key Storage page, click Use AD RMS centrally managed key storage, and then click
Next.
16. On the Cluster Key Password page, type Pa55w.rd twice, and then click Next.
17. On the Cluster Web Site page, verify that Default Web Site is selected, and then click Next.
18. On the Cluster Address page, provide the following information, and then click Next:
o Connection Type: Use an unencrypted connection (http://)
o Fully Qualified Domain Name: adrms.adatum.com
o Port: 80
Note: This lab uses port 80 for convenience. In production environments, you would help to
protect Active Directory Rights Management Services (AD RMS) by using an encrypted connection.
19. On the Licensor Certificate page, type AdatumADRMS, and then click Next.
20. On the SCP Registration page, click Register the SCP now, and then click Next.
21. On the Confirmation page, click Install, and then click Close.
22. In Server Manager, click Tools, and then click Internet Information Services (IIS) Manager.
23. In the Internet Information Services (IIS) Manager console, expand LON-SVR1\Sites
\Default Web Site, and then click _wmcs.
24. In the middle pane, double-click Authentication, click Anonymous Authentication, and then, in the
Actions pane, click Enable.
25. In the Connections pane, expand _wmcs, and then click licensing.
26. In the middle pane, double-click Authentication, click Anonymous Authentication, and then, in the
Actions pane, click Enable. Close the Internet Information Services (IIS) Manager console.
Note: You will not enable Anonymous Authentication in a production environment. This is
just to make the configuration easier in the lab.
27. On the Start screen, click Administrator icon on the left side of the menu, and then click Sign Out.
Note: You must sign out before you can manage AD RMS.
 Task 3: Configure the AD RMS Super Users group
1. Sign in to LON-SVR1 as Adatum\Administrator by using the password Pa55w.rd.
2. Open Server Manager, click Tools, and then click Active Directory Rights Management Services.
3. In the AD RMS console, expand the lon-svr1 (Local) node, and then click Security Policies.
4. In the Security Policies area, under Super Users, click Change super user settings.
5. In the Actions pane, click Enable Super Users.
6. In the Super Users area, click Change super user group.
7. In the Super Users dialog box, in the Super user group box, type
ADRMS_SuperUsers@adatum.com, and then click OK.
Exercise 2: Configuring AD RMS templates
 Task 1: Configure a new rights policy template
1. Ensure that you are signed in to LON-SVR1.
2. In the AD RMS console, click the Rights Policy Templates node.
3. In the Actions pane, click Create Distributed Rights Policy Template.
4. In the Create Distributed Rights Policy Template Wizard, on the Add Template Identification
information page, click Add.
5. On the Add New Template Identification Information page, provide the following information,
click Add, and then click Next:
o Language: English (United States)
o Name: ReadOnly
o Description: Read-only access. No copy or print.
6. On the Add User Rights page, click Add.
7. On the Add User or Group page, type executives@adatum.com, and then click OK.
8. When executives@adatum.com is selected, under Rights for executives@adatum.com, click View.
Verify that Grant owner (author) full control right with no expiration is selected, and then click
Next.
9. On the Specify Expiration Policy page, select the following settings, and then click Next:
o Content Expiration: Expires after the following duration (days): 7
o Use license expiration: Expires after the following duration (days): 7
10. On the Specify Extended Policy page, click Require a new use license every time content is
consumed (disable client-side caching), and then click Next.
11. On the Specify Revocation Policy page, click Finish.
 Task 2: Configure the rights policy template distribution
1. On LON-SVR1, click Start, and then click Windows PowerShell.
2. At the Windows PowerShell command prompt, type the following command, and then press Enter:
New-Item c:\rmstemplates -ItemType Directory
3. At the Windows PowerShell command prompt, type the following command, and then press Enter:
New-SmbShare -Name RMSTEMPLATES -Path c:\rmstemplates -FullAccess ADATUM\ADRMSSVC
4. At the Windows PowerShell command prompt, type the following command, and then press Enter:
New-Item c:\docshare -ItemType Directory
5. At the Windows PowerShell command prompt, type the following command, and then press Enter:
New-SmbShare -Name docshare -Path c:\docshare -FullAccess Everyone
6. Type exit, and then press Enter to exit Windows PowerShell.
7. Switch to the AD RMS console, click the Rights Policy Templates node, and then, in the Distributed
Rights Policy Templates area, click Change distributed rights policy templates file location
In the Rights Policy Templates dialog box, click Enable export.
9. In the Specify templates file location (UNC) box, type \\LON-SVR1\RMSTEMPLATES, and then
click OK.
10. On the taskbar, click File Explorer.
11. Navigate to the C:\rmstemplates folder, and then verify that ReadOnly.xml is present.
12. Close the File Explorer window.
 Task 3: Configure an exclusion policy
1. On LON-SVR1, switch to the AD RMS console, click the Exclusion Policies node, and then click
Manage application exclusion list.
2. In the Actions pane, click Enable Application Exclusion.
3. In the Actions pane, click Exclude Application.
4. In the Exclude Application dialog box, type the following information, and then click Finish:
o Application File name: Powerpnt.exe
o Minimum version: 14.0.0.0
o Maximum version: 16.0.0.0
5. Close the AD RMS console.
Results: After completing this exercise, you should have configured AD RMS templates.
Exercise 3: Using AD RMS on clients
 Task 1: Create a rights-protected document
1. Sign in to LON-CL1 as Adatum\Aidan by using the password Pa55w.rd.
2. Click Start, type Internet, and then click Internet Explorer. In the Internet Explorer window, rightclick the toolbar, click Menu bar, click Tools, and then select Internet options. If the Set up Internet
Explorer 11 window appears, select Use recommended security and compatibility settings, and
then click OK.
3. In the Internet options dialog box, click Security, click Local intranet, click Sites, click Advanced,
and then, under Add this website to the zone, type http://adrms.adatum.com. Click Add, click
Close, and then click OK two times.
Note: Note that you added adrms.adatum.com to the local intranet sites to achieve a single
sign on experience when signing in to the AD RMS servers.
4. Close Internet Explorer. If you receive a prompt, click Close all tabs.
5. On the Start menu, type Word, and then, in the results area, click Word 2016. If the First things first
window appears, click Ask me later, and then click Accept. If the Welcome to your new Office
window appears, close it.
6. In the Microsoft Word 2016 app, click Blank document
In the Word document, type the following text: This document is for executives only, and it should
not be modified. Click File, click Protect Document, click Restrict Access, and then click Read Only.
Note: If the ReadOnly template does not appear, you might need to first click Connect to
Rights Management Servers and get templates. After 20-30 seconds try again.
8. Click Save, and then click Browse.
9. In the Save As dialog box, save the document to the \\lon-svr1\docshare location with the name
Executives Only.docx.
10. Close Word 2016.
11. Click the Start menu, click the Aidan Norman icon, and then click Sign out.
 Task 2: Verify internal access to AD RMS-protected content as an authorized user
1. Sign in to LON-CL1 as Adatum\Holly by using the password Pa55w.rd.
2. Click Start, type Internet, and then click Internet Explorer. If the Set up Internet Explorer 11 window
appears, select Use recommended security and compatibility settings, and then click OK. In the
Internet Explorer window, right-click the toolbar, click Menu bar, click Tools, and then select
Internet options.
3. In Internet options, click Security, click Local intranet, click Sites, click Advanced, and then, under
Add this website to the zone, type http://adrms.adatum.com. Click Add, click Close, and then click
OK twice.
4. Close Internet Explorer. If you receive a prompt, click Close all tabs.
5. On the taskbar, click the File Explorer icon.
6. In the File Explorer window, navigate to \\lon-svr1\docshare.
7. In the docshare folder, double-click the Executives Only document.
8. When the document opens, verify that you are unable to modify or save the document. If the First
things first window appears in Word, click Ask me later, and then click Accept. If the Welcome to
your new Office window appears, close it.
9. Select a line of text in the document, right-click it, and then verify that you cannot make changes.
10. Click View Permission, review the permissions, and then click OK. You can see that Holly has only the
View permission. She is a member of the Executives group and can access the content.
11. Close Word 2016.
12. Click the Start screen, click the Holly Spencer icon, and then click Sign Out.
 Task 3: Open the rights-protected document as an unauthorized user
1. Sign in to LON-CL1 as Adatum\Harry by using the password Pa55w.rd.
2. Click Start, type Internet, and then click Internet Explorer. If the Set up Internet Explorer 11 window
appears, select Use recommended security and compatibility settings, and then click OK. In the
Internet Explorer window, right-click the toolbar, click Menu bar, click Tools, and then select
Internet options.
3. In Internet options, click Security, click Local intranet, click Sites, click Advanced, and then, under
Add this website to the zone, type http://adrms.adatum.com. Click Add, click Close, and then click
OK twice.
Close Internet Explorer. If you receive a prompt, click Close all tabs.
5. On the taskbar, click the File Explorer icon.
6. In the File Explorer window, navigate to \\lon-svr1\docshare.
7. In the docshare folder, double-click the Executives Only document, and then click OK in the
Microsoft Word window.
8. Verify that Harry is unable to open the document. Note that Harry cannot open the document because
the document is protected with an RMS template that allows only the Executives group to view the
document. If the First things first window appears in Word, click Ask me later, and then click Accept.
If the Welcome to your new Office window appears, close it.
9. Close Word 2016.
10. Click to Start screen, click the Harry Lawrence icon, and then click Sign Out.
```
