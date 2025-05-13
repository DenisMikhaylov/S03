```
Task 1: Enable ICMPv4 traffic
1. On LON-CL1, switch to Windows Firewall with Advanced Security.
2. In the left pane, click Inbound Rules, right-click Inbound Rules, and then click New Rule.
3. In the New Inbound Rule Wizard window, select Custom, and then click Next.
4. On the Program page, click Next.
5. On the Protocol and Ports page, in the Protocol type list, click ICMPv4 and then click Next.
6. On the Scope page, click Next.
7. On the Action page, click Allow the connection, and then click Next.
8. On the Profile page, click Next.
9. On the Name page, in the Name box, type Inbound ICMPv4 and then click Finish.
10. Minimize the Windows Firewall with Advanced Security window.
11. Switch to LON-SVR1.
12. Right-click Start, and then click Control Panel.
13. Click System and Security, and then click Windows Firewall.
14. Click Advanced settings, and then repeat steps 2 through 10.
 Task 2: Verify that communications are not secure
1. On LON-SVR1, in the Ask me anything box on the taskbar, type PowerShell, and then click Windows
PowerShell.
2. In the Administrator: Windows PowerShell window, type ping LON-CL1, and then press Enter.
Verify that the ping generated four “Reply from 172.16.0.40: bytes=32 time=xms TTL=128” messages.
Note that the times that the message lists may vary from the example.
3. Switch to Windows Firewall with Advanced Security.
4. In the left pane, expand Monitoring, and then expand Security Associations.
5. Click Main Mode, and then examine the information in the center pane. No information should be
present.
6. Click Quick Mode, and then examine the information in the center pane. No information should be
present.
7. Switch to LON-CL1.
8. In the Ask me anything box on the taskbar, type PowerShell, and then click Windows PowerShell.
9. To examine the Main Mode Security Associations (SAs), at the Windows PowerShell prompt, type
the following cmdlet, and then press Enter:
Get-NetIPsecMainModeSA
10. To examine the Quick Mode SAs, at the Windows PowerShell prompt, type the following cmdlet,
and then press Enter:
Get-NetIPsecQuickModeSA
Running each command should produce no result.
 Task 3: Create the Connection Security Rule
1. On LON-CL1, switch to Windows Firewall with Advanced Security.
2. In the left pane, click Connection Security Rules.MCT USE ONLY. STUDENT USE PROHIBITED
Installing and Configuring Windows 10 L4-29
3. In the Actions pane, click New Rule.
4. On the Rule Type page, verify that Isolation is selected, and then click Next.
5. On the Requirements page, select Require authentication for inbound connections and request
authentication for outbound connections, and then click Next.
6. On the Authentication Method page, click Computer and user (Kerberos V5), and then click
Next.
7. On the Profile page, click Next.
8. On the Name page, in the Name text box, type Authenticate all inbound connections, and then
click Finish.
9. Minimize the Windows Firewall with Advanced Security window.
10. Switch to LON-SVR1.
11. On LON-SVR1, switch to Windows Firewall with Advanced Security.
12. In the left pane, click Connection Security Rules.
13. In the Actions pane, click New Rule.
14. On the Rule Type page, verify that Isolation is selected, and then click Next.
15. On the Requirements page, select Require authentication for inbound connections and request
authentication for outbound connections, and then click Next.
16. On the Authentication Method page, click Computer and user (Kerberos V5), and then click
Next.
17. On the Profile page, click Next.
18. On the Name page, in the Name text box, type Authenticate all inbound connections, and then
click Finish.
19. Minimize the Windows Firewall with Advanced Security window.
 Task 4: Verify the rule, and monitor the connection
1. On LON-SVR1, in the Administrator: Windows PowerShell window, type ping LON-CL1, and then
press Enter. Verify that the ping generated four “Reply from 172.16.0.40: bytes=32 time=xms
TTL=128” messages. Note that the times that the message lists may vary from the example.
2. Switch to Windows Firewall with Advanced Security.
3. In the left pane, expand Monitoring, and then expand Security Associations.
4. Click Main Mode, and then examine the information in the center pane.
5. Click Quick Mode, and then examine the information in the center pane.
6. Close all open windows.
7. Switch to LON-CL1.
8. To examine the Main Mode Security Associations (SAs), at the Windows PowerShell command
prompt, type the following cmdlet, and then press Enter:
Get-NetIPsecMainModeSA
9. Review the result.MCT USE ONLY. STUDENT USE PROHIBITED
L4-30 Implementing network security
10. To examine the Quick Mode SAs, at the command prompt, type the following cmdlet, and then press
Enter:
Get-NetIPsecQuickModeSA
11. Review the result.
```
