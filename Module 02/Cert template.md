```
Lab: Deploying and using certificates
Exercise 1: Configuring certificate templates
 Task 1: Create a new template based on the Web Server template
1. On LON-DC1, in Server Manager, click Tools, and then click Certification Authority.
2. In the Certification Authority console, expand AdatumCA, right-click Certificate Templates, and
then select Manage.
3. In the Certificate Templates Console, locate the Web Server template in the list, right-click it, and
then click Duplicate Template.
4. Click the General tab, in the Template display name text box, type Production Web Server, and
then type 3 in the Validity period text box.
5. Click the Request Handling tab, select Allow private key to be exported, and then click OK.
Minimize the Certificate Templates Console.
6. In the Certification Authority console on LON-DC1, right-click Revoked Certificates, select All
tasks, click Publish, and then click OK.
 Task 2: Create a new template for users that includes smart card sign in
1. On LON-DC1, in Server Manager, click Tools, and then click Certification Authority.
2. Expand AdatumCA, right-click Certificate Templates, and then click Manage. In the Certificate
Templates Console, right-click the User certificate template, and then click Duplicate Template.
3. In the Properties of New Template dialog box, click the General tab, and then in the Template
display name text box, type Adatum User.
4. On the Subject Name tab, clear both the Include e-mail name in subject name and the E-mail
name check boxes.
5. On the Extensions tab, click Application Policies, and then click Edit.
6. In the Edit Application Policies Extension dialog box, click Add.
7. In the Add Application Policy dialog box, select Smart Card Logon, and then click OK twice.
8. Click the Superseded Templates tab, click Add, click the User template, and then click OK.
9. On the Security tab, click Authenticated Users. Under Permissions for Authenticated Users, select
the Allow check boxes for Read, Enroll, and Autoenroll, and then click OK.
10. Close the Certificate Templates Console.
 Task 3: Configure templates so that they can be issued
1. On LON-DC1, in the Certification Authority console, right-click Certificate Templates, point to
New, and then click Certificate Template to Issue.
2. In the Enable Certificate Templates window, hold the Ctrl key and click both Adatum User and
Production Web Server. Then click OK
Task 4: Enroll the Web Server certificate on LON-SVR2
1. Switch to LON-SVR2.
2. Click Start, and then click the Windows PowerShell icon.
3. At the command prompt in the Windows PowerShell command-line interface, type gpupdate /force,
and then press Enter.
4. Click Start, and then click Server Manager. From Server Manager, click Tools, and then click
Internet Information Services (IIS) Manager.
5. In the IIS console, click LON-SVR2, and then in the central pane, double-click Server Certificates.
6. In the Actions pane, click Create Domain Certificate.
7. On the Distinguished Name Properties page, complete the following fields, and then click Next:
o Common name: lon-svr2.adatum.com
o Organization: Adatum
o Organizational unit: IT
o City/locality: Seattle
o State/province: WA
o Country
o region: US
8. On the Online Certification Authority page, click Select, click AdatumCA, and then click OK.
9. In the Friendly name text box, type lon-svr2, and then click Finish.
10. Ensure that the certificate displays in the Server Certificates console.
11. In the IIS console, expand LON-SVR2, expand Sites, and then click Default Web Site.
12. In the Actions pane, click Bindings.
13. In the Site Bindings window, select Add.
14. In the Add Site Binding window, select https from the Type drop-down list. In the SSL certificate
drop-down list, click lon-svr2, click OK, and then click Close.
15. Close Internet Information Services (IIS) Manager.
16. Switch to LON-CL1. In the Cortana search field, type Internet Explorer. Click Internet Explorer in the
search results returned.
17. In Internet Explorer, type https://lon-svr2.adatum.com in the address bar, and then press Enter.
18. Ensure that the Internet Information Services page opens and that no certificate error displays
Exercise 2: Enrolling and using certificates
 Task 1: Configure autoenrollment for users
1. On LON-DC1, in Server Manager, click Tools, and then click Group Policy Management.
2. Expand Forest: Adatum.com, expand Domains, expand Adatum.com, right-click Default Domain
Policy, and then click Edit.
3. Expand User Configuration, expand Policies, expand Windows Settings, expand Security Settings,
and then click to highlight Public Key Policies.
4. In the details pane, double-click Certificate Services Client – Auto-Enrollment.
5. In the Configuration Model drop-down list, click Enabled, select Renew expired certificates,
update pending certificates, and remove revoked certificates and Update certificates that use
certificate templates, and then click OK to close the properties window.
6. In the right pane, double-click the Certificate Services Client – Certificate Enrollment Policy object.
7. On the Enrollment Policy tab, set the Configuration Model to Enabled, and then ensure that the
Certificate Enrollment Policy list displays the Active Directory Enrollment policy. It should have a
check mark next to it and display a status of Enabled. Click OK to close the window.
8. Close both the Group Policy Management Editor window and the Group Policy Management
console.
 Task 2: Verify autoenrollment
1. On LON-CL1, click Start, type PowerShell, and then click the Windows PowerShell icon.
2. At the Windows PowerShell command prompt, type gpupdate /force, and then press Enter.
3. After the policy refreshes, type mmc.exe, and then press Enter.
4. In Console1, click File, click Add/Remove Snap-in, click Certificates, click Add, click Finish, and then
click OK.
5. Expand Certificates – Current User, expand Personal, and then click Certificates.
6. Verify that a certificate based on the Adatum User template is issued for Administrator. To verify the
name of the template, scroll to the right in the console window.
7. Close Console1 without saving changes.
8. Sign out of LON-CL1.
 Task 3: Configure the enrollment agent for smart card certificates
1. On LON-DC1, in Server Manager, click Tools, and then open Certification Authority.
2. In the certsrv console, expand AdatumCA, right-click Certificate Templates, and then click Manage.
3. In the Certificate Templates Console, double-click Enrollment Agent.
4. Click the Security tab, and then click Add.
5. In the Select Users, Computers, Service Accounts, or Groups window, type Annie, click Check
Names, and then click OK.
6. On the Security tab, click Annie Conner, select the Allow check box for Read and Enroll permissions,
and then click OK.
7. Close the Certificate Templates Console.
In the certsrv console, right-click Certificate Templates, point to New, and then click Certificate
Template to Issue.
9. In the list of templates, click Enrollment Agent, and then click OK.
10. Switch to LON-CL1, and then sign in as Adatum\Annie with the password Pa55w.rd.
11. Click Start, type Command Prompt, and then press Enter. In the Command Prompt window, type
mmc.exe, and then press Enter.
12. In Console1, click File, and then click Add/Remove Snap-in.
13. Click Certificates, click Add, and then click OK.
14. Expand Certificates – Current User, expand Personal, click Certificates, right-click Certificates,
point to All Tasks, and then click Request New Certificate.
15. In the Certificate Enrollment Wizard, on the Before You Begin page, click Next.
16. On the Select Certificate Enrollment Policy page, click Next.
17. On the Request Certificates page, select Enrollment Agent, click Enroll, and then click Finish.
18. Sign out of LON-CL1.
19. Switch to LON-DC1.
20. In the Certification Authority console, right-click AdatumCA, and then click Properties.
21. On the Enrollment Agents tab, click Restrict Enrollment agents.
22. On the pop-up window that displays, click OK.
23. In the Enrollment agents section, click Add.
24. In the Select User, Computer or Group field, type Annie, click Check Names, and then click OK.
25. Click Everyone, and then click Remove.
26. In the Certificate Templates section, click Add.
27. In the list of templates, select Adatum User, and then click OK.
28. In the Certificate Templates section, click <All>, and then click Remove.
29. In the Permission section, click Add.
30. In the Select User, Computer or Group field, type Marketing, click Check Names, and then
click OK.
31. In the Permission section, click Everyone, click Remove, and then click OK.
 Task 4: Use certificates for digital signing of a Microsoft Office document
1. On LON-CL1, sign in as Adatum\Administrator with the password Pa55w.rd.
2. Click the Start button, type Word 2016, and then click Word 2016.
Note: If you receive a prompt from the Microsoft Office Activation Wizard, click
Close. If prompted to update, select Ask me later, and then click Accept.
3. Click blank document, type some text, and then save the document to the desktop.
4. On the toolbar, click INSERT, and then in the Text pane, in the Signature Line drop-down list, click
Microsoft Office Signature Line.
In the Signature Setup window, type your name in the Suggested signer text box, type
Administrator in the Suggested signer’s title text box, type Administrator@adatum.com in the
Suggested signer’s email address text box, and then click OK.
6. Right-click the signature line in the document, and then click Sign….
7. In the Sign window, click Change.
8. In the Windows Security window under Select a certificate, select the Administrator certificate with
today’s date, and then click OK.
9. In the text box to the right of the X, type your name, click Sign, and then click OK. Instead of typing
your name, you also can select an image. This image can be your scanned handwriting signature.
10. Ensure that you cannot edit the document further.
Note: Try to type some text in the document.
11. Close Microsoft Word 2016, and then save changes if you receive a prompt.
12. Sign out of LON-CL1.
Exercise 3: Configuring and implementing key recovery
 Task 1: Configure the certification authority to issue KRA certificates
1. On LON-DC1, in the Certification Authority console, expand the AdatumCA node, right-click the
Certificates Templates folder, and then click Manage.
2. In the details pane, right-click the Key Recovery Agent certificate, and then click Properties.
3. In the Key Recovery Agent Properties dialog box, click the Issuance Requirements tab, and then
clear the CA certificate manager approval check box.
4. Click the Security tab. Notice that Domain Admins and Enterprise Admins are the only groups that
have the Enroll permission, and then click OK.
5. Close the Certificate Templates Console.
6. In the Certification Authority console, right-click Certificate Templates, point to New, and then
click Certificate Template to Issue.
7. In the Enable Certificate Templates dialog box, click the Key Recovery Agent template, and then
click OK.
8. Close the Certification Authority console.
 Task 2: Acquire the KRA certificate
1. On LON-DC1, click Start, and then click the Windows PowerShell icon.
2. At the Windows PowerShell command prompt, type mmc.exe, and then press Enter.
3. In the Console1-[Console Root] console, click File, and then click Add/Remove Snap-in.
4. In the Add or Remove Snap-ins dialog box, click Certificates, and then click Add
In the Certificates snap-in dialog box, select My user account, click Finish, and then click OK.
6. Expand the Certificates - Current User node, right-click Personal, point to All Tasks, and then click
Request New Certificate.
7. In the Certificate Enrollment Wizard, on the Before You Begin page, click Next.
8. On the Select Certificate Enrollment Policy page, click Next.
9. On the Request Certificates page, select the Key Recovery Agent check box, click Enroll, and then
click Finish.
10. Refresh the console, and then view the Key Recovery Agent (KRA) in the personal store; scroll across the
certificate properties and verify that Certificate Template Key Recovery Agent is present.
11. Close Console1 without your saving changes.
 Task 3: Configure the CA to allow key recovery
1. On LON-DC1, in Server Manager, click Tools, and then click Certification Authority. In the
Certification Authority console, right-click AdatumCA, and then click Properties.
2. In the AdatumCA Properties dialog box, click the Recovery Agents tab, and then select Archive the
key.
3. Under Key recovery agent certificates, click Add.
4. In the Key Recovery Agent Selection dialog box, click More Choices and click the certificate with the
KRA purpose (it most likely will be last on the list issued to Administrator), and then click OK twice.
5. When prompted to restart the certification authority (CA), click Yes.
 Task 4: Configure a custom template for key archival
1. On LON-DC1, in the Certification Authority console, expand AdatumCA. Right-click the Certificates
Templates folder, and then click Manage.
2. In the Certificate Templates Console, right-click the User certificate, and then click Duplicate
Template.
3. In the Properties of New Template dialog box, on the General tab, in the Template display name
text box, type Archive User.
4. On the Request Handling tab, select the Archive subject's encryption private key check box.
5. If a pop-up window displays, click OK.
6. Click the Subject Name tab, clear the E-mail name and Include E-mail name in subject name check
boxes, and then click OK.
7. Close the Certificate Templates Console.
8. In the Certification Authority console, right-click the Certificates Templates folder, point to New,
and then click Certificate Template to Issue.
9. In the Enable Certificate Templates dialog box, click the Archive User template, and then
click OK.
10. Close the Certification Authority console.
 Task 5: Verify key archival functionality
1. Sign in to LON-CL1 as Adatum\Aidan with the password Pa55w.rd.
2. On the Start screen, type mmc.exe, and then press Enter. If prompted, click Yes in the User Account
Control window.
In the Console1-[Console Root] console, click File, and then click Add/Remove Snap-in.
4. In the Add or Remove Snap-ins dialog box, click Certificates, click Add, and then click OK.
5. Expand the Certificates - Current User node, right-click Personal, click All Tasks, and then click
Request New Certificate.
6. In the Certificate Enrollment Wizard, on the Before You Begin page, click Next.
7. On the Select Certificate Enrollment Policy page, click Next.
8. On the Request Certificates page, select the Archive User check box, click Enroll, and then click
Finish.
9. Refresh the console, then expand Personal and click Certificates. Note that a certificate is issued to
Aidan based on the Archive User certificate template.
10. Simulate the loss of a private key by deleting the certificate. In the central pane, right-click the
certificate that you just enrolled, select Delete, and then click Yes to confirm.
11. Switch to LON-DC1.
12. Open the Certification Authority console, expand AdatumCA, and then click the Issued Certificates
store.
13. In the details pane, double-click a certificate with a Requestor Name of Adatum\Aidan and a
Certificate Template name of Archive User.
14. Click the Details tab, copy the Serial number, and then click OK. You might copy the number either
by selecting it and pressing Ctrl+C or by noting it in a document.
15. Click the Start button, and then click the Windows PowerShell icon.
16. At the Windows PowerShell command prompt, type the following command, where <serial number>
is the serial number that you copied, and then press Enter:
Certutil –getkey <serial number> outputblob
Note: If you copy and paste the serial number, remove the spaces between the numbers
or enclose the serial number between double quotes.
17. Verify that the Outputblob file now displays in the C:\Users\Administrator folder.
18. To convert the Outputblob file into a .pfx file, at the Windows PowerShell command prompt, type
the following command, and then press Enter:
Certutil –recoverkey outputblob aidan.pfx
19. When prompted for the new password, type Pa55w.rd, and then confirm the password.
20. After the command executes, close Windows PowerShell.
21. Go to C:\Users\Administrator, and then verify that aidan.pfx—the recovered key—is created.
22. Switch to LON-CL1.
23. Open File Explorer, and then browse to \\LON-DC1.adatum.com\c$. When prompted for
credentials, use Adatum\Administrator with the password Pa55w.rd.
24. Go to \\LON-DC1.adatum.com\c$\users\administrator
Right-click the aidan.pfx file, and then select Copy. Go to C:\Users\aidan. In the empty space, rightclick, and then select Paste.
26. Double-click the aidan.pfx file.
27. On the Welcome to the Certificate Import Wizard page, click Next.
28. On the File to Import page, click Next.
29. On the Password page, type the password Pa55w.rd, and then click Next.
30. On the Certificate Store page, click Next, click Finish, and then click OK.
31. In Console1, expand the Certificates - Current User node, expand Personal, and then click
Certificates.
32. Refresh the console, and then verify that the certificate for Aidan is restored.
