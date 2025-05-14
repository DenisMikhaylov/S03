```
Lab A: Implementing WSUS and
deploying updates
Exercise 1: Implementing WSUS
 Task 1: Install the WSUS server role
1. Sign in to LON-SVR4 as Adatum\Administrator with the password Pa55w.rd.
2. On LON-SVR4, if necessary, open Server Manager, click Manage, and then click Add Roles and
Features.
3. In the Add Roles and Features Wizard, click Next.
4. On the Select installation type page, ensure that Role-based or feature-based installation is
selected, and then click Next.
5. On the Select destination server page, click Next.
6. On the Select server roles page, select the Windows Server Update Services check box.
7. In the pop-up window, click Add Features.
8. On the Select server roles page, click Next.
9. On the Select features page, click Next.
10. On the Windows Server Update Services page, click Next.
11. On the Select role services page, confirm that both WID Connectivity and WSUS Services are
selected, and then click Next.
12. On the Content location selection page, in the text box, type C:\WSUSUpdates, and then click
Next.
13. On the Web Server Role (IIS) page, click Next.
14. On the Select role services page, click Next.
15. On the Confirm installation selections page, click Install.
16. When the installation completes, click Close.
17. In Server Manager, click Tools, and then click Windows Server Update Services.
18. In the Complete WSUS Installation dialog box, click Run, and wait for the task to complete. Click
Close.
19. Do not close the Windows Server Update Services Configuration Wizard:LON-SVR4 window.
 Task 2: Configure WSUS to synchronize with an upstream WSUS server
1. In the Windows Server Update Services Configuration Wizard:LON-SVR4 window, click Next
twice.
2. On the Choose Upstream Server page, click Synchronize from another Windows Server Update
Services server, and in the Server name text box, type LON-SVR2.Adatum.com, and then click
Next.
3. On the Specify Proxy Server page, click Next.
4. On the Connect to Upstream Server page, click Start Connecting. Wait for the upstream server
settings to be applied, and then click Next.
5. On the Choose Languages page, click Next.
6. On the Set Sync Schedule page, click Next.
7. On the Finished page, select the Begin initial synchronization check box, and then click Finish.
8. In the Update Services console, in the navigation pane, double-click LON-SVR4, and then click
Options.
9. In the Options pane, click Computers.
10. In the Computers dialog box, select Use Group Policy or registry settings on computers. Click OK.
Note: You might need to wait until synchronization is complete before you can click OK.
Results: After completing this exercise, you should have implemented the Windows Server Update
Services (WSUS) server role.
Exercise 2: Configuring update settings
 Task 1: Configure WSUS groups
1. On LON-SVR4, in the Update Services console, in the navigation pane, double-click Computers.
2. Click All Computers, and then in the Actions pane, click Add Computer Group.
3. In the Add Computer Group dialog box, in the Name text box, type Research, and then click Add.
 Task 2: Configure Group Policy to deploy WSUS settings
1. Switch to LON-DC1.
2. In Server Manager, click Tools, and then click Group Policy Management.
3. In the Group Policy Management console, double-click Forest: Adatum.com, double-click
Domains, and then double-click Adatum.com.
4. Right-click the Research organizational unit (OU), and then click Create a GPO in this domain, and
Link it here.
5. In the New GPO dialog box, in the Name text box, type WSUS Research, and then click OK.
6. Double-click the Research OU, right-click WSUS Research, and then click Edit.
Note: If the Group Policy Management Console dialog box appears, click OK to
continue.
7. In the Group Policy Management Editor, under Computer Configuration, double-click Policies,
double-click Administrative Templates, double-click Windows Components, and then click
Windows Update.
8. In the Settings pane, double-click Configure Automatic Updates, and then click the Enabled
option.
9. In the Configure automatic updating field, click and select 4 – Auto download and schedule the
install, and then click OK.
10. In the Settings pane, double-click Specify intranet Microsoft update service location, and then
click the Enabled option.
11. In the Set the intranet update service for detecting updates and the Set the intranet statistics
server text boxes, type http://LON-SVR4.Adatum.com:8530, and then click OK.
12. In the Settings pane, double-click Enable client-side targeting.
13. In the Enable client-side targeting dialog box, click the Enabled option, and in the Target group
name for this computer text box, type Research, and then click OK.
14. Close the Group Policy Management Editor and the Group Policy Management console.
15. In Server Manager, click Tools, and then click Active Directory Users and Computers.
16. In Active Directory Users and Computers, double-click Adatum.com, click Computers, right-click
LON-CL1, and then click Move.
17. In the Move dialog box, click the Research OU, and then click OK.
18. Close Active Directory Users and Computers.
 Task 3: Verify the application of Group Policy settings
1. Switch to LON-CL1.
2. On LON-CL1, in Cortana’s search box, type Updates, and then click Windows Update settings.
3. Click Advanced options, and then clear the Defer feature updates check box. Click the back button
and then close the Update settings window.
4. Click the Start button, click Power, and then click Restart.
5. After LON-CL1 restarts, sign in as Adatum\Administrator with the password Pa55w.rd.
6. In Cortana’s search box, type cmd, right-click the Command Prompt tile, and then click Run as
administrator.
7. At the command prompt, type the following command, and then press Enter:
Gpresult /r
8. In the output of the command, confirm that, under Computer Settings, WSUS Research is listed
under Applied Group Policy Objects.
 Task 4: Initialize Windows Update
1. On LON-CL1, at the command prompt, type the following command, and then press Enter:
Wuauclt.exe /detectnow /reportnow
2. Switch to LON-SVR4.
3. In the Update Services console, expand Computers, expand All Computers, and then click
Research.
4. In the Status drop-down list, click Any, and then click Refresh.
5. Verify that LON-CL1 appears in the Research group. If it does not, then repeat steps 1 through 3,
and then click Refresh. It might take several minutes for LON-CL1 to display.MCT USE ONLY. STUDENT USE PROHIBITED
L12-80 Managing, monitoring, and maintaining virtual machine installations
6. Verify that updates are reported as needed. If not, repeat steps 1-3. It might take 10 to 15 minutes for
updates to register. Click Refresh every few minutes as you wait.
Results: After completing this exercise, you should have configured update settings for client computers.
Exercise 3: Approving and deploying an update by using WSUS
 Task 1: Approve WSUS updates for the Research computer group
1. On LON-SVR4, in the Update Services console, under Updates, click All Updates.
2. Scroll to the bottom of the list of updates, right-click Cumulative Update for Windows 10 Version
1607 for x64-based Systems (KB3201845), and then click Approve.
3. In the Approve Updates window, in the Research drop-down list box, select Approved for Install.
4. Click OK, and then click Close.
 Task 2: Deploy updates to LON-CL1
1. On LON-CL1, at the command prompt, type the following command, and then press Enter:
Wuauclt.exe /detectnow
2. In Cortana’s search box, type Windows Update.
3. In the Best match list, click Check for updates.
4. Click Check for updates.
5. The update begins to download.
Note: If the Update status reports that then device is up to date, wait 5 minutes and check
for updates again. The update will not be available to LON-CL1 until LON-SVR4 has downloaded
the update from LON-SVR2.
6. When the update has been downloaded, click Install Now.
Note: The update installation can take 10-15 minutes.
7. Close the Windows Update window when the installation is complete, and restart the computer.
8. After LON-CL1 restarts, sign in as Adatum\Administrator with the password Pa55w.rd.
 Task 3: Verify update deployment to LON-CL1
1. On LON-CL1, in Cortana’s search box, type Event Viewer, and then click View event logs.
2. In Event Viewer, expand Applications and Services Logs, expand Microsoft, expand Windows,
expand WindowsUpdateClient, and then click Operational to view events.
3. Confirm that events are logged in relation to the update.
```
