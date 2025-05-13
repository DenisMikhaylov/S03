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
