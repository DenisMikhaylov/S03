```
Managing data security
Exercise 1: Using BitLocker
 Task 1: Configure GPO settings
1. Sign in to LON-CL1 as Adatum\Administrator with the password Pa55w.rd.
2. In the Ask me anything box on the taskbar, type gpedit.msc, and then press Enter.
3. In Local Group Policy Editor, under Computer Configuration node, expand Administrative
Templates, expand Windows Components, and then expand BitLocker Drive Encryption.
4. Click Operating System Drives, and then double-click Require additional authentication at
startup.
5. In the Require additional authentication at startup dialog box, click Enabled, and then click OK.
6. Close Local Group Policy Editor.
7. Right-click Start, and then click Command Prompt (Admin).
8. At the command prompt, type gpupdate /force, and then press Enter.
9. Close all open windows.
10. Restart LON-CL1.
11. After the computer restarts, sign in as Adatum\Administrator with the password Pa55w.rd.
 Task 2: Enable BitLocker
1. On LON-CL1, in the Ask me anything box on the taskbar, type bitlocker, and then click Manage
BitLocker.
2. Click Allfiles (E:) BitLocker off, and then click Turn on BitLocker.
3. In the BitLocker Drive Encryption (E:) dialog box, click Use a password to unlock the drive.
4. In the Enter your password and Reenter your password text boxes, type Pa55w.rd, and then click
Next.
5. On the How do you want to back up your recovery key? page, click Save to a file.
6. In the Save BitLocker recovery key as dialog box, click Local Disk (C:).
7. On the File Explorer toolbar, click New folder, type BitLocker, and then press Enter.
8. In the Save BitLocker recovery key as dialog box, click Open, click Save, click Yes, and then click
Next.
9. On the Choose which encryption mode to use page, ensure that New encryption mode (best for
fixed drives on this device) is selected, and then click Next.
10. On the BitLocker Drive Encryption (E:) page, click Start encrypting.
11. After the encryption process is complete, restart LON-CL1.
 Task 3: Verify BitLocker
1. Sign in to LON-CL1 as Adatum\Administrator with the password Pa55w.rd.
2. On the taskbar, click File Explorer.
3. In the navigation pane, click This PC.MCT USE ONLY. STUDENT USE PROHIBITED
L10-68 Securing Windows 10
4. Right-click Local Disk (E:), click Open, verify that the drive is listed as not accessible and that access is
denied, and then click OK.
5. In the Ask me anything box on the taskbar, type bitlocker, and then click Manage BitLocker.
6. Click E: BitLocker on (Locked), and then click Unlock Drive.
7. Enter the password Pa55w.rd, press Enter to unlock the drive, and then verify access to the drive
contents.
8. Close all open windows
```
