UAK
```
Configure UAC settings with Group Policy
In this task, you will use Group Policy to configure the UAC settings.
1. On the Lon-dc1 , log on.
2. In Server Manager, click Tools, and select Active Directory Administrative Center.
3. Select the Tree View and navigate to adatum.com, Computers.
4. Right‐click Echo and select Move, then select adatum.com, Accounts, Sales as the destination, and
click OK.
5. Close Active Directory Administrative Center.
6. Open Server Manager, click Tools and select Group Policy Management
Navigate to adatum.com, 
8. Right‐click on domain, and then select the Create a GPO in this domain, and Link it here
option.
9. Type Sales UAC Settings in the Name box, and then click OK.
10. Right‐click Sales UAC Settings, and then select the Edit option.
11. Navigate to Computer Configuration, Policies, Windows Settings, Security Settings, Local
Policies, Security Options.
12. Scroll down to the bottom in the right section of window to see all the User Account Control
related options.
13. Drag the line between the Policy column heading and the Policy Settings column heading to
the right to maximize the Policy column until all the headings are exposed.
14. Double‐click the following policy: User Account Control: Behavior of the elevation prompt for
standard users.
15. List the options for the elevation prompt.
16. Is it possible to prevent standard users from being prompted for alternate credentials?
17. Click the Cancel button to close the window.
18. Double‐click the following policy: User Account Control: Behavior of the elevation prompt for
administrators in Admin Approval Mode.
19. List the options for the prompt behavior.
20. Can administrators in Admin Approval Mode be treated like standard users?
21. Select the Define this policy setting check box.
22. Select Prompt for consent on the secure desktop from the drop‐down menu, and then click
OK.
Note
Setting this option is effectively the same as configuring the Always Notify option
for UAC in Control Panel on the local machine.
Double‐click the User Account Control: Admin Approval Mode for the Built‐in Administrator
account.
24. List the options for this setting.
25. What would be the impact of enabling this option?
26. Which UAC setting can you configure to block standard users from installing applications?
27. Which UAC setting can you configure to only allow applications that have a signing
certificate?
28. Click the Cancel button.
29. Close the Group Policy Management Editor but leave the Group Policy Management Console
open
```
applocker
```
Task 1: Prepare the Admin console for the AppLocker
demonstration
In this task, you will configure an application for use with AppLocker. To configure and
application to be allowed or blocked by Applocker the Admin Console must have access to the
files that are going to be used. For this reason, you will need to install the software on the Admin
Console itself first.
1. Log on to the Echo VM as Speck with the password of Pa$$w0rd.
2. Mount the GroupPolicy‐LabFiles.iso using the lab interface.
3. Open File Explorer and browse to the D:\LabFiles\Install folder.
4. Double‐click the Defraggler.exe file to install it.
5. Click Yes on the UAC prompt.
6. Click Next in the Welcome window.
7. On the Install Options screen, clear the Replace Windows Disk Defragmenter option.
8. Click Next.
9. Clear the Install Google Chrome and Also include Google Toolbar check boxes, then click
Install.
10. Clear the Run Defraggler and View Release Notes check boxes, and then click Finish.
Task 2: Prepare the client for the AppLocker demonstration
In this task, you will prepare the client VM for the AppLocker demonstration. This will be the
machine to be affected by the Applocker policy.
1. Log on to the Delta VM as Speck with the password of Pa$$w0rd.
2. Mount the GroupPolicy‐LabFiles.iso using the lab interface.
3. Open File Explorer and browse to the D:\LabFiles\Install folder.
4. Double‐click the Defraggler.exe file to install it.
5. Click Yes on the UAC prompt.
6. Click Next in the Welcome window.
7. On the Install Options screen, clear the Replace Windows Disk Defragmenter option.
8. Click Next.
9. Clear the Install Google Chrome and Also include Google Toolbar check boxes, then click
Install.
10. Clear the Run Defraggler and View Release Notes check boxes, and then click Finish.
Task 3: Configure the Application Identity Service
The Application Identity Service must be running on all target Windows 7 or later computers if
the AppLocker policies are going to affect them.
In this task, you will configure the Application Identify Service.
1. On the Echo VM, open the Server Manager and click Tools, Group Policy Management.
2. Navigate to the hq.local\Accounts OU.
3. Right‐click the Accounts OU and select Create a GPO in this domain, and Link it here to create
a new GPO.
4. In the new GPO dialog box, type AppIdentity Service in the Name box, and then click OK.
5. Right‐click the AppIdentity Service GPO and select Edit.
6. Under Computer Configuration, expand Policies, Windows Settings, Security Settings, and
System Services.
7. Double‐click Application Identity and then select the Define this policy setting check box.
8. Choose Automatic, and then click OK.
9. Close the Group Policy Management Editor, but leave the Group Policy Management Console
open.
Task 4: Create a New AppLocker policy
In this task, you will create a new AppLocker policy.
1. In the Group Policy Management console, navigate to the hq.local\Accounts OU.
2. Right‐click the Accounts OU and select Create a GPO in this domain, and Link it here to create
a new GPO.
3. In the New GPO dialog box, type AppLocker Policy in the Name box, and then click OK.
4. Right‐click the AppLocker Policy GPO and select Edit.
5. Under Computer Configuration, expand Policies, Windows Settings, Security Settings,
Application Control Policies.
6. Click AppLocker.
7. In the right window, click the Configure rule enforcement link.
8. Under Executable rules, select the Configured check box, then click OK.
9. Expand AppLocker, Executable Rules.
10. Right‐click Executable Rules in the left section of the window and select Create Default Rules.
11. Right‐click Executable Rules in the left section of the window and select Create New Rule.
12. Click Next in the Before You Begin window. (If you cannot see the Next button, you will need
to auto‐hide the taskbar, or drag the taskbar to the right of your screen.)
13. Select the Deny radio button, and then click the Select button.
14. Type Sales Users in the Enter the object name to select box, click OK, and then click Next.
15. Select the Publisher option, and then click Next.
16. Click the Browse button and navigate to C:\Program Files\Defraggler.
17. Click the Defraggler64.exe file, and then click Open.
18. What version of the file will be blocked?
19. What file name will be blocked?
20. Slide the slider bar up to Product name.
21. Now what version and file name will be blocked?
22. Click Next.
23. Click Next in the Exceptions window.
24. Click Create to create the rule.
25. Click No when you are asked to create the Default Rules.
26. Close the Group Policy Management Editor.
```
SCM
```
Using the Security Compliance
Manager
This is a bonus exercise to be completed if time permits.
Microsoft makes many Solution Accelerators available for free on their Web site. One of these
accelerators is the Security Compliance Manager. You can use this tool ensure that your
environment meets your security guidelines.
Note:
With the 1703 release of Windows 10, as of June 2017, Microsoft will no longer
continue development of the SCM. Instead, there is a new tool called the Policy
Analyzer. SCM will still be functional and available, but will not be enhanced or
supported any further. See Exercise 1 for the Policy Analyzer.
Task 1: Install the Security Compliance Manager
In this task, you will install the Security Compliance Manager.
1. On the Echo VM, mount the Windows 10 Client ISO image using the lab interface.
2. Log on to the Echo VM as Speck with a password of Pa$$w0rd.
3. Open PowerShell as Administrator.
4. Type the following command, and then press ENTER:
Enable‐WindowsOptionalFeature ‐FeatureName NetFx3 ‐online ‐Source
D:\Sources\sxs ‐LimitAccess
(Wait for a few minutes until the installation is complete.)Managing Windows Environments with Group Policy Lab Guide
132 © Global Knowledge Training LLC
5. On the Echo VM, mount the GroupPolicy‐LabFiles‐2014.iso image using the lab interface.
6. Open File Explorer and browse to the D:\LabFiles\Install\GroupPolicy folder.
7. Double‐click SecurityComplianceManager.exe.
8. Click Yes if UAC prompts you to continue.
9. Select the I have read and accept the license terms check box, then click Install.
10. Click Finish to complete the Visual C++ Redistributable setup.
11. Deselect the "Always check for updates…" checkbox, then click Next in the Welcome window.
12. Select the I accept the terms of the license agreement radio button and then click Next.
13. Accept the default location and then click Next.
14. Click Next on the SQL Server 2008 Express screen.
15. Select the I accept the terms in the license agreement radio button and then click Next.
16. Click Install to begin the installation. (If a program compatibility message appears, click Run
the program without getting help.)
17. Click Finish to complete the installation. (It will take several minutes for the Finish option to
appear.)
Task 2: Examine the Baselines
In this task, you will examine the Security Compliance Manager Baselines.
1. If the Security Compliance Manager does not automatically open, go to the Start screen and
click the Security Compliance Manager icon. (The first time it launches, it may take a few
minutes to import the basellines.)
2. In the middle window, click Download Microsoft Baselines Automatically.
3. Click Download.
4. Click Run on all of the Security Warning messages that appear.
5. Click Next, then click Import.
6. In the left window pane, expand Windows Server 2012.
7. Select the Hyper‐V Security baseline and browse through the settings.
8. Examine some of the other baselines and settings.
9. Select the File Server Security baseline, then click the Compare/Merge link in the right hand
window.
10. Choose the Windows Server 2012, DNS Server Security baseline to compare it with.
11. Click OK to start the comparison.
12. How many settings are different?Lab 6: Securing Windows Using Group Policy
© Global Knowledge Training LLC 133
13. How many settings are the same?
14. Close the comparison window.
Task 3: Examine the current configuration against a baseline
In this task, you will compare the current Windows Domain environment against a baseline.
1. Open the Server Manager, then click Tools, Group Policy Management.
2. Expand Forest: hq.local, Domains, hq.local, Group Policy Objects.
3. Right‐click the Default Domain Policy and select Back Up.
4. Click Browse and expand This PC, Local Disk (C:).
5. Select Local Disk (C:) and click Make New Folder.
6. Type DefaultDomainPolicy for the folder name and click OK.
7. Click Back Up.
8. Click OK.
9. Switch back to the Security Compliance Manager console.
10. In the right‐window pane, select the GPO Backup (folder) link in the Import area.
11. Browse to the This PC, Local Disk (C:), DefaultDomainPolicy folder and select the GUID folder
name, then click OK.
12. In the Baseline Name box, type hq.local ‐ Default Domain Policy and click OK.
13. Click OK when the import is finished.
14. Browse through the settings that were imported.
15. Select the Compare/Merge link in the right‐window pane.
16. Select the Windows Server 2016, WS2016 Domain Security Compliance baseline, then click
OK.
17. What settings are different?
18. Click Close when you are finished analyzing the comparison.
19. In the hq.local ‐ Default Domain Policy baseline, click Maximum password age and change the
value to 60 days, then click Collapse.Managing Windows Environments with Group Policy Lab Guide
134 © Global Knowledge Training LLC
Task 4: Export a baseline for use as a policy
In this task, you will export a baseline to be used as a Group Policy.
1. In Security Compliance Manager, select the hq.local ‐ Default Domain Policy.
2. In the right‐window pane, click the GPO Backup (folder) link in the Export area.
3. Browse to Local Disk (C:) and click Make New Folder, then type BaselineDomainPolicy and
click OK.
4. Switch to the Group Policy Management console.
5. Expand Forest: hq.local, Domains, hq.local, Group Policy Objects.
6. Open the Group Policy Objects container and right‐click the Default Domain Policy.
7. Select the Import Settings option.
8. Click Next, then Next again.
9. Click Browse on the Backup Location screen and navigate to the C:\BaselineDomainPolicy
folder, then click OK.
10. Click Next.
11. Click Next on the Source GPO screen.
12. Click Next twice, then click Finish.
13. Click OK when the Import is finished.
14. Select the Default Domain Policy, then click the Settings tab.
15. Expand Policies, Windows Settings, Security Settings, Account Policies.
16. What is the Maximum Password Age?

```
