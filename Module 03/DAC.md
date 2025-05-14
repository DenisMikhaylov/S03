Lab: Implementing Secure Data Access
```
Exercise 1: Preparing for DAC Deployment
 Task 1: Prepare AD DS for DAC deployment
1. On LON-DC1, in Server Manager, click on Tools, and then click Active Directory Domains and
Trusts.
2. In the Active Directory Domains and Trusts console, right-click Adatum.com and select Raise
Domain Functional Level.
3. In the Raise domain functional level window, in the Select an available domain functional level
window, select Windows Server 2012 and click Raise.
4. Click OK twice.
5. Right-click Active Directory Domains and Trusts [LON-DC1.Adatum.com] and click Raise Forest
Functional Level….
6. In the Raise forest functional level window, in the Select an available forest functional level
window, select Windows Server 2012 and click Raise.
7. Click OK twice.
8. Close Active Directory Domains and Trusts console.
9. On LON-DC1, in Server Manager, click Tools, and then click Active Directory Users and Computers.
10. In Active Directory Users and Computers, right-click Adatum.com, click New, and then click
Organizational Unit.
11. In the New Object – Organizational Unit dialog box, in the Name field, type DAC-Protected, and
then click OK.
12. Click the Computers container.
13. Right-click the LON-SVR1 and then click Move.
14. In the Move window, click DAC-Protected, and then click OK.
15. Repeat steps 13 and 14 for the LON-CL1 computer.
16. Close Active Directory Users and Computers.
17. On LON-DC1, in Server Manager, click Tools, and then click Group Policy Management.
18. Expand Forest: Adatum.com, expand Domains, and then expand Adatum.com.
19. Click the Group Policy Objects container.
20. In the results pane, right-click Default Domain Controllers Policy, and then click Edit.
21. In the Group Policy Management Editor, under Computer Configuration, expand Policies, expand
Administrative Templates, expand System, and then click KDC.
22. In the details pane, double-click KDC support for claims, compound authentication and Kerberos
armoring.
23. In the KDC support for claims, compound authentication and Kerberos armoring window, select
Enabled, in the Options section, click the drop-down list box, select Always provide claims, and
then click OK.MCT USE ONLY. STUDENT USE PROHIBITED
L3-26 Configuring Advanced Windows Server® 2012 Services
24. Close Group Policy Management Editor and the Group Policy Management Console.
25. On the taskbar, click the Windows PowerShell icon.
26. In the Windows PowerShell window, type gpupdate /force, and then press Enter. After Group Policy
updates, close Windows PowerShell.
27. On LON-DC1, in Server Manager, click Tools, and then click Active Directory Users and Computers.
28. Expand Adatum.com, right-click Users, click New, and then click Group.
29. In the Group name field, type ManagersWKS, and then click OK.
30. Click the DAC-Protected container, right-click LON-CL1, and then click Properties.
31. Click the Member Of tab, and then click Add.
32. In Select Groups window, type ManagersWKS, click Check Names, and then click OK twice.
33. Click the Managers OU, right-click Aidan Delaney, and then click Properties.
34. In the Aidan Delaney Properties window, click the Organization tab. Ensure that the Department
field is populated with the value Managers, and then click Cancel.
35. Click the Research OU, right-click Allie Bellew, and then click Properties.
36. In the Allie Bellew Properties window, click the Organization tab. Ensure that the Department field
is populated with the value Research, and then click Cancel.
37. Close Active Directory Users and Computers.
 Task 2: Configure user and device claims
1. On LON-DC1, click Tools, and then click Active Directory Administrative Center.
2. In the Active Directory Administrative Center, in the navigation pane, click Dynamic Access Control,
and then double-click Claim Types.
3. In the Claim Types container, in the Tasks pane, click New, and then click Claim Type.
4. In the Create Claim Type window, in the Source Attribute section, select department.
5. In the Display name text box, type Company Department.
6. Select both User and Computer check boxes.
7. Scroll down to Suggested Values section and select The following values are suggested: option.
8. Click Add….
9. In the Add a suggested value window, type Managers in both Value and Display name fields, and
click OK.
10. Click Add….
11. In the Add a suggested value window, type Research in both Value and Display name fields, and
click OK.
12. Click OK.
13. In the Active Directory Administrative Center, in the Tasks pane, click New, and then select Claim
Type.
14. In the Create Claim Type window, in the Source Attribute section, click description.
15. Clear the User check box, select the Computer check box, and then click OK.MCT USE ONLY. STUDENT USE PROHIBITED
L3-27
 Task 3: Configure resource properties and resource property lists
1. In the Active Directory Administrative Center, click Dynamic Access Control.
2. In the central pane, double-click Resource Properties.
3. In the Resource properties list, right-click Department, and then click Enable.
4. In the Resource properties list, right-click Confidentiality, and then click Enable.
5. In the Resource Property List, ensure that both the Department and Confidentiality properties are
enabled.
6. Double-click Department, scroll down to the Suggested Values section, and then click Add.
7. In the Add a suggested value window, in both Value and Display name text boxes, type Research,
and then click OK twice.
8. Click Dynamic Access Control, and then double-click Resource Property Lists.
9. In the central pane, double-click Global Resource Property List, ensure that both Department and
Confidentiality display, and then click Cancel. If they do not display, click Add, add these two
properties, and then click OK.
10. Close the Active Directory Administrative Center.
 Task 4: Implement file classifications
1. On LON-SVR1, in Server Manager, click Tools, and then click File Server Resource Manager.
2. In File Server Resource Manager, expand Classification Management.
3. Select and right-click Classification Properties, and then click Refresh.
4. Verify that Confidentiality and Department properties are listed.
5. Click Classification Rules, and in the Actions pane, click Create Classification Rule.
6. In the Create Classification Rule window, for the Rule name, type Set Confidentiality.
7. Click the Scope tab, and then click Add.
8. In the Browse For Folder dialog box, expand Local Disk (C:), click the Docs folder, and then click
OK.
9. Click the Classification tab. Make sure that the following settings are set, and then click Configure:
• Classification method: Content Classifier
• Property: Confidentiality
• Value: High
10. In the Classification Parameters dialog box, click the Regular expression drop-down list box, and
then click String.
11. In the Expression field next to the word String, type secret, and then click OK.
12. Click the Evaluation Type tab, select Re-evaluate existing property values, click Overwrite the
existing value, and then click OK.
13. In File Server Resource Manager, in the Actions pane, click Run Classification with all rules now.
14. Click Wait for classification to complete, and then click OK.
15. After the classification is complete, you will be presented with a report. Verify that two files were
classified. You can confirm this in the Report Totals section.MCT USE ONLY. STUDENT USE PROHIBITED
L3-28 Configuring Advanced Windows Server® 2012 Services
16. Close the report.
17. On the taskbar, click the File Explorer icon.
18. In the File Explorer window, expand drive C:, and then expand the Docs folder.
19. In the Docs folder, right-click Doc1.txt, click Properties, and then click the Classification tab. Verify
that Confidentiality is set to High.
20. Repeat step 19 on files Doc2.txt and Doc3.txt. Doc2.txt should have same Confidentiality as Doc1.txt,
while Doc3.txt should have no value. This is because only Doc1.txt and Doc2.txt have the word
“secret” in their content.
 Task 5: Assign a property to the Research folder
1. On LON-SVR1, open File Explorer, and browse to Local Disk (C:).
2. Right-click the Research folder, and then click Properties.
3. Click Classification tab.
4. Click Department.
5. In the Value section, click Research. Click Apply.
6. Click OK.
Results: After completing this exercise, you will have prepared Active Directory® Domain Services (AD DS)
for Dynamic Access Control (DAC) deployment, configured claims for users and devices, and configured
resource properties to classify files.MCT USE ONLY. STUDENT USE PROHIBITED
L3-29
Exercise 2: Implementing DAC
 Task 1: Configure central access rules
1. On LON-DC1, in Server Manager, click Tools, and then click Active Directory Administrative
Center.
2. In the Active Directory Administrative Center, in the navigation pane, click Dynamic Access Control,
and then double-click Central Access Rules.
3. In the Tasks pane, click New, and then click Central Access Rule.
4. In the Create Central Access Rule dialog box, in the Name field, type Department Match.
5. In the Target Resources section, click Edit.
6. In the Central Access Rule dialog box, click Add a condition.
7. Set a condition as follows: Resource-Department-Equals-Value-Research, and then click OK.
8. In the Permissions section, click Use following permissions as current permissions.
9. In the Permissions section, click Edit.
10. Remove permission for Administrators.
11. In Advanced Security Settings for Permissions, click Add.
12. In Permission Entry for Permissions, click Select a principal.
13. In the Select User, Computer, Service Account, or Group window, type Authenticated Users, click
Check Names, and then click OK.
14. In the Basic permissions section, select the Modify, Read and Execute, Read and Write check boxes.
15. Click Add a condition and then click the Group drop-down list box, and then click Company
Department.
16. Click the Value drop-down list box, and then click Resource.
17. In the last drop-down list box, click Department. Click OK three times.
Note: You should have this expression as a result: User-Company Department-EqualsResource-Department.
18. In the Tasks pane, click New, and then click Central Access Rule.
19. For the name of the rule, type Access Confidential Docs.
20. In the Target Resources section, click Edit.
21. In the Central Access Rule window, click Add a condition.
22. In the last drop-down list box, click High. Click OK.
23. Note: You should have this expression as a result: Resource-Confidentiality-Equals-ValueHigh.
24. In the Permissions section, click Use following permissions as current permissions.
25. In the Permissions section, click Edit.
26. Remove permission for Administrators.
27. In Advanced Security Settings for Permissions, click Add.MCT USE ONLY. STUDENT USE PROHIBITED
L3-30 Configuring Advanced Windows Server® 2012 Services
28. In Permission Entry for Permissions, click Select a principal.
29. In the Select User, Computer, Service Account, or Group window, type Authenticated Users, click
Check Names, and then click OK.
30. In the Basic permissions section, select the Modify, Read and Execute, Read, and Write check boxes.
31. Click Add a condition. Set the first condition to: User-Company Department-Equals-ValueManagers, and then click Add a condition.
32. Set the second condition to: Device-Group-Member of each-Value-ManagersWKS. Click OK three
times.
Note: If you cannot find ManagersWKS in the last drop-down list box, click Add items.
Then in the Select User, Computer, Service Account, or Group window, type ManagersWKS, click
Check Names, and then click OK.
 Task 2: Configure central access policies
1. On LON-DC1, in the Active Directory Administrative Center, click Dynamic Access Control, and then
double-click Central Access Policies.
2. In the Tasks pane, click New, and then click Central Access Policy.
3. In the Name field, type Protect confidential docs, and then click Add.
4. Click the Access Confidential Docs rule, click >>, and then click OK twice.
5. In the Tasks pane, click New, and then click Central Access Policy.
6. In the Name field, type Department Match, and then click Add.
7. Click the Department Match rule, click >>, and then click OK twice.
8. Close the Active Directory Administrative Center.
 Task 3: Apply central access policies to a file server
1. On LON-DC1, in Server Manager, click Tools, and then click Group Policy Management.
2. In the Group Policy Management Console, under Domains, expand Adatum.com, right-click DACProtected, and then click Create a GPO in this domain, and link it here.
3. Type DAC Policy, and then click OK.
4. Right-click DAC Policy, and then click Edit.
5. Expand Computer Configuration, expand Policies, expand Windows Settings, expand Security
Settings, expand File System, right-click Central Access Policy, and then click Manage Central
Access Policies.
6. Press and hold the Ctrl button, and click both Department Match and Protect confidential docs,
click Add, and then click OK.
7. Close the Group Policy Management Editor and the Group Policy Management Console.
8. On LON-SVR1, on the taskbar, click the Windows PowerShell icon.
9. At a Windows PowerShell command prompt, type gpupdate /force, and then press Enter. Wait until
Group Policy is updated.
10. Close Windows PowerShell when you get the message that both Computer and User policies update
completed successfully.MCT USE ONLY. STUDENT USE PROHIBITED
L3-31
11. On the taskbar, click the File Explorer icon.
12. In File Explorer, browse to Local Disk (C:), right-click the Docs folder, and then click Properties.
13. In the Properties dialog box, click the Security tab, and then click Advanced.
14. In the Advanced Security Settings for Docs window, click the Central Policy tab, and then click
Change.
15. In the drop-down list box, select Protect confidential docs. Ensure that in the Applies to dropdown box, the value This folder, subfolders and files is selected, and then click OK twice.
16. Right-click the Research folder, and then click Properties.
17. In the Research Properties dialog box, click the Security tab, and then click Advanced.
18. In the Advanced Security Settings for Research window, click the Central Policy tab, and then click
Change.
19. In the drop-down list box, click Department Match. Ensure that in the Applies to drop-down box,
the value This folder, subfolders and files is selected, and then click OK twice.
Results: After completing this exercise, you will have implemented DAC.MCT USE ONLY. STUDENT USE PROHIBITED
L3-32 Configuring Advanced Windows Server® 2012 Services
Exercise 3: Validating and Remediating DAC
 Task 1: Access file resources as an approved user
1. Start LON-CL1 and LON-CL2 virtual machines.
2. Sign in on LON-CL1 as Adatum\Allie with the password Pa$$w0rd.
3. Click the Desktop tile, and then on the taskbar, click the File Explorer icon.
4. In the File Explorer address bar, type \\LON-SVR1\Research, and then press Enter.
5. Because Allie is a member of the Research team, verify that you can access this folder and open the
documents inside.
6. Sign out of LON-CL1.
7. Sign in to LON-CL1 as Adatum\Aidan with the password Pa$$w0rd.
8. Click the Desktop tile, and then on the taskbar, click the File Explorer icon.
9. In the File Explorer address bar, type \\LON-SVR1\Docs.
10. Verify that you can access this folder and open all the files inside.
11. Sign out of LON-CL1.
 Task 2: Access file resources as an unapproved user
1. Sign in to LON-CL2 as Adatum\Aidan with the password Pa$$w0rd.
2. Click the Desktop tile, and then on the taskbar, click the File Explorer icon.
3. In the File Explorer address bar, type \\LON-SVR1\Docs. You should be unable to view Doc1.txt or
Doc2.txt, because LON-CL2 is not permitted to view secret documents.
4. Sign out of LON-CL2.
5. Sign in to LON-CL2 as Adatum\April with the password Pa$$w0rd.
6. Click the Desktop tile, and then on the taskbar, click the File Explorer icon.
7. In the File Explorer address bar, type \\LON-SVR1\Docs, and then press Enter.
8. In the Docs folder, try to open Doc3.txt. You should be able to open that document. Close Notepad.
9. In the File Explorer address bar, type \\LON-SVR1\Research, and then press Enter. You should be
unable to access the folder.
10. Sign out of LON-CL2.
 Task 3: Evaluate user access with DAC
1. On LON-SVR1, on the taskbar, click the File Explorer icon.
2. In the File Explorer window, navigate to C:\Research, right-click Research, and then click Properties.
3. In the Properties dialog box, click the Security tab, click Advanced, and then click Effective Access.
4. Click select a user, and in the Select User, Computer, Service Account, or Group window, type April,
click Check Names, and then click OK.
5. Click View effective access, and then review the results. The user April should not have access to this
folder.
6. Click Include a user claim, and then in the drop-down list box, click Company department.MCT USE ONLY. STUDENT USE PROHIBITED
L3-33
7. In the Value drop-down box, select Research, and then click View Effective access. April should
now have access.
8. Close all open windows.
 Task 4: Configure access-denied remediation
1. On LON-DC1, in Server Manager, click Tools, and then click Group Policy Management.
2. In the Group Policy Management Console, expand Forest: Adatum.com, expand Domains, expand
Adatum.com, and then click Group Policy objects.
3. Right-click DAC Policy, and then click Edit.
4. Under Computer Configuration, expand Policies, expand Administrative Templates, expand
System, and then click Access-Denied Assistance.
5. In the details pane, double-click Customize Message for Access Denied errors.
6. In the Customize Message for Access Denied errors window, click Enabled.
7. In the Display the following message to users who are denied access text box, type You are
denied access because of permission policy. Please request access.
8. Select the Enable users to request assistance check box.
9. Review the other options, but do not make any changes, and then click OK.
10. In the details pane of the Group Policy Management Editor, double-click Enable access-denied
assistance on client for all file types, click Enabled, and then click OK.
11. Close the Group Policy Management Editor and the Group Policy Management Console.
12. Switch to LON-SVR1, and on the taskbar, click the Windows PowerShell icon.
13. At the Windows PowerShell command prompt, type gpupdate /force, and then press Enter. Wait
until Group Policy is updated.
 Task 5: Request access remediation
1. Sign in to LON-CL1 as Adatum\April with the password Pa$$w0rd.
2. Click the Desktop tile, and then on the taskbar, click the File Explorer icon.
3. In the File Explorer address bar, type \\LON-SVR1\Research, and then press Enter. You should be
unable to access the folder.
4. Click Request assistance. Review the options for sending a message, and then click Close.
5. Sign out of LON-CL1.
Results: After completing this exercise, you will have validated DAC functionality.MCT USE ONLY. STUDENT USE PROHIBITED
L3-34 Configuring Advanced Windows Server® 2012 Services
Exercise 4: Implementing Work Folders
 Task 1: Install Work Folders functionality, configure SSL certificate, and create
WFSync group
1. On LON-SVR2, in Server Manager, click Add roles and features.
2. On the Before you begin page, click Next.
3. On the Select installation type page, ensure that Role - based or feature - based installation is
selected, and then click Next.
4. On the Select destination server page, click Next.
5. On the Select server roles page, expand File and Storage Services (1 of 2 installed), expand File
and iSCSI Services, and then select Work Folders.
6. In the Add features that are required for Work Folders dialog box, note the features, and then
click Add Features.
7. On the Select server roles page, click Next.
8. On the Select features page, click Next.
9. On the Confirm installation selection pages, click Install.
10. When the installation finishes, click Close.
11. In the Server Manager on LON-SVR2, click Tools, and then click Internet Information Services
(IIS) Manager.
12. In the Internet Information Services (IIS) Manager console, click on LON-SVR2, click No when
prompted, and then double click Server Certificates in the middle pane.
13. In the Actions pane, click Create Domain Certificate.
14. In the Create Certificate window, fill in the text fields as follows:
a. Common name: lon-svr2.adatum.com
b. Organization: Adatum
c. Organizational unit: IT
d. City/locality: Seattle
e. State/province: WA
f. Country/region: US
15. Click Next.
16. On the Online Certification Authority page, click Select.
17. In the Select Certification Authority window, select AdatumCA and click OK.
18. In the Friendly name text box, type lon-svr2.adatum.com and click Finish. (Note: If you receive an
error, restart the LON-DC1 machine, and then repeat this step.)
19. In the IIS console, expand Sites, and then click on Default Web Site.
20. In the Actions pane, click Bindings.
21. In the Site Bindings window, click Add….
22. In the Add Site Binding window, under Type, select https. In the SSL certificate drop-down list,
select lon-svr2.adatum.com.MCT USE ONLY. STUDENT USE PROHIBITED
L3-35
23. Click OK, and then click Close.
24. Close Internet Information Services (IIS) Manager.
25. Switch to LON-DC1.
26. On LON-DC1, in Server Manager, click Tools, and then click Active Directory Users and Computers.
27. Expand Adatum.com, right-click Users, click New, and then click Group.
28. In the Group name field, type WFSync, and then click OK.
29. Click the Managers OU, right-click Aidan Delaney, and then click Properties.
30. Click the Member Of tab, and then click Add.
31. In Select Groups window, type WFSync, click Check Names, and then click OK twice.
 Task 2: Provision a share for Work Folders
1. On LON-SVR2, in Server Manager, in the navigation pane, click File and Storage Services.
2. Click Shares, and in the SHARES area, click Tasks, and then select New Share….
3. In the New Share Wizard, on the Select the profile for this share page, ensure that SMB Share –
Quick is selected, and then click Next.
4. On the Select the server and path for this share page, accept the defaults, and then click Next.
5. On the Specify share name page, in the Share name field, type WF-Share, and then click Next.
6. On the Configure share settings page, select Enable access - based enumeration, leave the other
settings at their defaults, and then click Next.
7. On the Specify permissions to control access page, note the default settings, and then click Next.
8. On the Confirm selections page, click Create.
9. On the View results page, click Close.
 Task 3: Configure and implement Work Folders
1. On LON-SVR2, in Server Manager, expand File and Storage Services, and then click Work Folders.
2. In the WORK FOLDERS tile, click Tasks, and then click New Sync Share….
3. In the New Sync Share Wizard, on the Before you begin page, click Next.
4. On the Select the server and path page, select Select by file share, ensure that the share you
created in the previous task (WF-Share) is highlighted, and then click Next.
5. On the Specify the structure for user folders page, accept the default selection (user alias), and
then click Next.
6. On the Enter the sync share name page, accept the default, and then click Next.
7. On the Grant sync access to groups page, note the default selection to disable inherited
permissions and grant users exclusive access, and then click Add.
8. In the Select User or Group dialog box, in the Enter the object names to select field, type WFsync,
click Check Names, and then click OK.
9. On the Grant sync access to groups page, click Next.
10. On the Specify device policies page, note the selections, accept the default selection, and then click
Next.
11. On the Confirm selections page, click Create.MCT USE ONLY. STUDENT USE PROHIBITED
L3-36 Configuring Advanced Windows Server® 2012 Services
12. On the View results page, click Close.
13. Switch to LON-DC1.
14. Open Server Manager, click Tools, and then click Group Policy Management.
15. Expand Forest: Adatum.com-Domains-Adatum.com, and then click Group Policy Objects. Rightclick Group Policy Objects, and then click New.
16. In the New GPO window, type Work Folders GPO in the Name field, and then click OK.
17. Right-click Work Folders GPO, and then click Edit.
18. In the Group Policy Management Editor, expand User Configuration \Policies\Administrative
Templates\Windows Components, and then click Work Folders.
19. Double-click Specify Work Folders settings in the details pane, and in the Specify Work Folders
settings dialog box, click Enabled.
20. In the Work Folders URL text box, type https://lon-svr2.adatum.com, and then select Force
automatic setup.
21. Click OK to close the Specify Work Folders settings dialog box, and then close the Group Policy
Management Editor.
22. In the Group Policy Management Console, right-click the Adatum.com domain object, and then
select Link an Existing GPO….
23. In the Select GPO window, select Work Folders GPO, and then click OK.
24. Close the Group Policy Management Console.
 Task 4: Validate Work Folders functionality
1. Sign in to LON-CL1 as Adatum\Aidan with the password Pa$$w0rd.
2. On Start screen, start typing PowerShell, and then click the Windows PowerShell icon in the Search
pane.
3. At the Windows PowerShell command prompt, type gpupdate /force, and then press Enter.
4. Open File Explorer and navigate to This PC.
5. Verify that the WorkFolders folder is created.
Note: The presence of the Work Folders folder indicates that the Work Folders
configuration is successful.
6. In File Explorer, create a few text files in the Work Folders folder.
Note: File Explorer displays the synchronization status of the files in the Work Folders folder.
7. Right-click the Windows button on the taskbar, and then click Control Panel.
8. In Control Panel, click System and Security, and then click Work Folders.
9. Click Apply policies. Click Yes.
10. Ensure that Work Folders are configured and working.
11. Close the Control Panel.
12. Sign in to LON-CL2 as Adatum\Aidan with the password Pa$$word.MCT USE ONLY. STUDENT USE PROHIBITED
L3-37
13. On Start screen, start typing PowerShell, and then click the Windows PowerShell icon in the Search
pane.
14. At the Windows PowerShell command prompt, type gpupdate /force, and then press Enter.
15. Open File Explorer and navigate to This PC.
16. Verify that the WorkFolders folder is created.
17. Right-click the Windows button on the taskbar, and then click Control Panel.
18. In Control Panel, click System and Security, and then click Work Folders.
19. Click Apply policies. Click Yes.
20. Open the Work Folders folder and verify that the files that you created on LON-CL1 are present.
```
