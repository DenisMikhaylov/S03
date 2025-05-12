```
Exercise 1: Deploying a Stand-Alone Root CA
Task 1: Install and configure Active Directory Certificate Services on **LON-Svr4**
1. Sign in to LON-SVR4 as Administrator with the password Pa55w.rd.
2. In the Server Manager, click Add roles and features.
3. On the Before You Begin page, click Next.
4. On the Select installation type page, click Next.
5. On the Select destination server page, click Next.
6. On the Select server roles page, select Active Directory Certificate Services. When the Add Roles
and Features Wizard displays, click Add Features, and then click Next.
7. On the Select features page, click Next.
8. On the Active Directory Certificate Services page, click Next.
9. On the Select role services page, ensure that Certification Authority is selected, and then click Next.
10. On the Confirm installation selections page, click Install.
11. On the Installation progress page, after installation completes successfully, click the text Configure
Active Directory Certificate Services on the destination server.
12. In the AD CS Configuration Wizard, on the Credentials page, click Next.
13. On the Role Services page, select Certification Authority, and then click Next.
14. On the Setup Type page, select Standalone CA, and then click Next.
15. On the CA Type page, ensure that Root CA is selected, and then click Next.
16. On the Private Key page, ensure that Create a new private key is selected, and then click Next.
17. On the Cryptography for CA page, keep the default selections for Cryptographic Service Provider
(CSP) and Hash Algorithm, but set the Key length to 4096, and then click Next.
18. On the CA Name page, in the Common name for this CA box, type AdatumRootCA, and then click
Next.
19. On the Validity Period page, click Next.
20. On the CA Database page, click Next.
21. On the Confirmation page, click Configure.
22. On the Results page, click Close.
23. On the Installation progress page, click Close.
24. On LON-SVR4, in Server Manager, click Tools, and then click Certification Authority.
25. In the certsrv – [Certification Authority (Local)] console, right-click AdatumRootCA, and then click
Properties.
26. In the AdatumRootCA Properties dialog box, click the Extensions tab.
27. On the Extensions tab, in the Select extension drop-down list box, click CRL Distribution Point
(CDP), and then click Add.
28. In the Location box, type http://lon-svr1.adatum.com/CertData/, in the Variable drop-down list
box, click <CaName>, and then click Insert.
29. In the Variable drop-down list box, click <CRLNameSuffix>, and then click Insert.
30. In the Variable drop-down list box, click <DeltaCRLAllowed>, and then click Insert.
31. In the Location box, position the cursor at the end of the URL, type .crl, and then click OK.
32. Select the following options, and then click Apply:
• Include in the CDP extension of issued certificates
• Include in CRLs. Clients use this to find Delta CRL locations
33. In the Certification Authority pop-up window, click No.
34. In the Select extension drop-down list box, click Authority Information Access (AIA), and then
click Add.
35. In the Location box, type http://lon-svr1.adatum.com/CertData/, in the Variable drop-down list
box, click <ServerDNSName>, and then click Insert.
36. In the Location box, type an underscore (_),in the Variable drop-down list box, click <CaName>,
and then click Insert. Position the cursor at the end of the URL.
37. In the Variable drop-down list box, click <CertificateName>, and then click Insert.
38. In the Location box, position the cursor at the end of the URL, type .crt, and then click OK.
39. Select the Include in the AIA extension of issued certificates check box, and then click OK.
40. Click Yes to restart the Certification Authority service.
41. In the Certification Authority console, expand AdatumRootCA, right-click Revoked Certificates,
point to All Tasks, and then click Publish.
42. In the Publish CRL window, click OK.
43. Right-click AdatumRootCA, and then click Properties.
44. In the AdatumRootCA Properties dialog box, click View Certificate.
45. In the Certificate dialog box, click the Details tab.
46. On the Details tab, click Copy to File.
47. In the Certificate Export Wizard, on the Welcome page, click Next.
48. On the Export File Format page, select DER encoded binary X.509 (.CER), and then click Next.
49. On the File to Export page, click Browse. In the File name box, type \\lon-svr1\C$, and then press
Enter.
50. In the File name box, type RootCA, click Save, and then click Next.
51. Click Finish, and then click OK three times.
52. Open a File Explorer window, and browse to C:\Windows\System32\CertSrv\CertEnroll.
53. In the Cert Enroll folder, click both files, right-click the highlighted files, and then click Copy
54. In the File Explorer address bar, type \\lon-svr1\C$, and then press Enter.
55. Right-click the empty space, and then click Paste.
56. Close File Explorer.

```
```
Exercise 2: Deploying an Enterprise Subordinate CA
 Task 1: Install and configure AD CS on LON-SVR1
1. Sign in to LON-SVR1 as Adatum\Administrator with the password Pa55w.rd.
2. In the Server Manager, click Add roles and features.
3. On the Before You Begin page, click Next.
4. On the Select installation type page, click Next.
5. On the Select destination server page, click Next.
6. On the Select server roles page, select Active Directory Certificate Services.
7. When the Add Roles and Features Wizard displays, click Add Features, and then click Next.
8. On the Select features page, click Next.
9. On the Active Directory Certificate Services page, click Next.
10. On the Select role services page, ensure that Certification Authority is selected already, and then
select Certification Authority Web Enrollment.
11. When the Add Roles and Features Wizard displays, click Add Features, and then click Next.
12. On the Confirm installation selections page, click Install.
13. On the Installation progress page, after installation is successful, click the text Configure Active
Directory Certificate Services on the destination server.
14. In the AD CS Configuration Wizard, on the Credentials page, click Next.
15. On the Role Services page, select both Certification Authority and Certification Authority Web
Enrollment, and then click Next.
16. On the Setup Type page, select Enterprise CA, and then click Next.
17. On the CA Type page, click Subordinate CA, and then click Next.
18. On the Private Key page, ensure that Create a new private key is selected, and then click Next.
19. On the Cryptography for CA page, keep the default selections, and then click Next.
20. On the CA Name page, in the Common name for this CA box, type Adatum-IssuingCA, and then
click Next.
21. On the Certificate Request page, ensure that Save a certificate request to file on the target
machine is selected, and then click Next.
22. On the CA Database page, click Next.
23. On the Confirmation page, click Configure.
24. On the Results page, click Close.
25. On the Installation progress page, click Close.
 Task 2: Install a subordinate CA certificate
1. On LON-SVR1, open a File Explorer window, and then navigate to Local Disk (C:).
2. Right-click RootCA.cer, and then click Install Certificate.
3. In the Certificate Import Wizard, click Local Machine, and then click Next.
4. On the Certificate Store page, click Place all certificates in the following store, and then click
Browse.
5. Select Trusted Root Certification Authorities, click OK, click Next, and then click Finish.
6. When the Certificate Import Wizard window appears, click OK.
7. In the File Explorer window, select the AdatumRootCA.crl and LON-CA1_AdatumRootCA.crt files,
right-click the files, and then click Copy.
8. Double-click inetpub.
9. Double-click wwwroot.
10. Create a new folder, and then name it CertData.
11. Paste the two copied files into that folder.
12. Switch to Local Disk (C:).
13. Right-click the file LON-SVR1.Adatum.com_Adatum-LON-SVR1-CA.req, and then click Copy.
14. In the File Explorer address bar, type \\LON-SVR4\C$, and then press Enter.
15. In the File Explorer window, right-click an empty space, and then click Paste. Make sure that the
request file is copied to LON-SVR4.
16. Switch to the LON-SVR4 server.
17. In the Certificate Authority console, right-click AdatumRootCA, point to All Tasks, and then click
Submit new request.
18. In the Open Request File window, navigate to Local Disk (C:), click file LONSVR1.Adatum.com_Adatum-LON-SVR1-CA.req, and then click Open.
19. In the Certification Authority console, click the Pending Requests container. Right-click Pending
Requests, and then click Refresh.
20. In the details pane, right-click the request (with ID 2), point to All Tasks, and then click Issue.
21. In the Certification Authority console, click the Issued Certificates container.
22. In the details pane, double-click the certificate, click the Details tab, and then click Copy to File.
23. In the Certificate Export Wizard, on the Welcome page, click Next.
24. On the Export File Format page, click Cryptographic Message Syntax Standard – PKCS #7
Certificates (.P7B), click Include all certificates in the certification path if possible, and then click
Next.
25. On the File to Export page, click Browse.
26. In the File name box, type \\lon-svr1\C$, and then press Enter.
27. In the File name box, type SubCA, click Save, click Next, click Finish, and then click OK twice.
28. Switch to LON-SVR1.
29. In the Server Manager, click Tools, and then click Certification Authority.
30. In the Certification Authority console, right-click Adatum-IssuingCA, point to All Tasks, and then
click Install CA Certificate.
31. Navigate to Local Disk (C:), click the SubCA.p7b file, and then click Open.
32. Wait for 15 to 20 seconds, and then on the toolbar, click the green icon to start the CA service.
33. Ensure that the CA starts successfully.
 Task 3: Publish the root CA certificate through Group Policy
1. On LON-DC1, on the taskbar, click the Server Manager icon.
2. In the Server Manager, click Tools, and then click Group Policy Management.
In the Group Policy Management Console, expand Forest: Adatum.com, expand Domains, expand
Adatum.com, right-click Default Domain Policy, and then click Edit.
4. In the Computer Configuration node, expand Policies, expand Windows Settings, expand Security
Settings, expand Public Key Policies, right-click Trusted Root Certification Authorities, click
Import, and then click Next.
5. On the File to Import page, click Browse.
6. In the file name box, type \\lon-svr1\C$, and then press Enter.
7. Click file RootCA.cer, and then click Open.
8. Click Next two times, and then click Finish.
9. When the Certificate Import Wizard window appears, click OK.
10. Close the Group Policy Management Editor and the Group Policy Management Console
