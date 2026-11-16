# IT Diagnostics Lab

---

## 📑 Table of Contents

* [Overview](#-overview)
* [Scenarios](#-scenarios)

---

## 🌐 Overview

This repository documents real-world IT support scenarios and how to resolve them step by step. Each scenario reflects common helpdesk tickets you would encounter in an entry-level IT support role. The goal is to build troubleshooting habits, practice documentation, and understand how to resolve issues efficiently.

---

## 🧩 Scenarios

---

### 1. 🔒 User Account Locked Out

**Problem:** A user cannot log in and receives an "Account is locked out" message.

**Steps to resolve:**
1. Open **Active Directory Users and Computers (ADUC)**
2. Search for the user's account
3. Right-click the account > **Properties** > **Account** tab
4. Check the **Unlock account** checkbox
5. Click **Apply** > **OK**
6. Ask the user to try logging in again
7. If it keeps locking, investigate failed login attempts in **Event Viewer** > Windows Logs > Security

---

### 2. 🔑 Password Reset Request

**Problem:** A user forgot their password and cannot log in.

**Steps to resolve:**
1. Verify the user's identity before making any changes
2. Open **ADUC** and search for the user
3. Right-click the account > **Reset Password**
4. Enter a temporary password
5. Check **User must change password at next logon**
6. Click **OK**
7. Communicate the temporary password to the user securely
8. Confirm the user can log in and set their new password

---

### 3. 🌐 No Internet Connection

**Problem:** A user reports they have no internet access but their computer is on.

**Steps to resolve:**
1. Ask the user to check if other devices on the same network have internet
2. On the affected machine, open **Command Prompt** and run:
   - `ipconfig` — check if the machine has a valid IP address
   - `ping 8.8.8.8` — test connectivity to Google's DNS
   - `ping google.com` — test DNS resolution
3. If no IP address, run `ipconfig /release` then `ipconfig /renew`
4. Restart the network adapter via **Device Manager**
5. If still not working, restart the router or escalate to the network team
6. Document the resolution

---

### 4. 🖨️ Printer Not Working

**Problem:** A user cannot print and gets an error or the job is stuck in the queue.

**Steps to resolve:**
1. Check that the printer is powered on and connected
2. On the user's machine, go to **Settings** > **Printers & Scanners**
3. Select the printer > **Open print queue**
4. Cancel all pending jobs in the queue
5. Restart the **Print Spooler** service:
   - Open **Services** (services.msc)
   - Find **Print Spooler** > right-click > **Restart**
6. Try printing a test page
7. If still failing, remove and re-add the printer
8. Reinstall the printer driver if needed

---

### 5. 💻 Computer Running Slow

**Problem:** A user complains their computer is very slow and unresponsive.

**Steps to resolve:**
1. Press **Ctrl + Shift + Esc** to open **Task Manager**
2. Click the **Performance** tab to check CPU, memory, and disk usage
3. Go to the **Processes** tab and identify any high-usage processes
4. End any unnecessary tasks by right-clicking > **End Task**
5. Check for malware by running a scan with **Windows Defender**
6. Disable startup programs: **Task Manager** > **Startup** tab > disable unneeded apps
7. Check available disk space — low storage can slow a computer significantly
8. Run **Disk Cleanup** to free up space
9. Restart the computer and check if performance improves
10. If hardware is too old, escalate for hardware upgrade consideration

---

### 6. 📶 Unable to Connect to Wi-Fi

**Problem:** A user's laptop cannot find or connect to the Wi-Fi network.

**Steps to resolve:**
1. Confirm the Wi-Fi is enabled — check the physical switch or function key (e.g., Fn + F2)
2. Click the **Wi-Fi icon** in the taskbar and check if the network appears
3. If the network appears but won't connect, right-click > **Forget** and reconnect
4. Open **Command Prompt** and run:
   - `netsh wlan show interfaces` — check adapter status
   - `ipconfig /flushdns` — clear DNS cache
5. Update the Wi-Fi adapter driver via **Device Manager**
6. Run the built-in **Network Troubleshooter**: Settings > System > Troubleshoot > Internet Connections
7. If no networks appear at all, restart the network adapter or check if the driver is missing

---

### 7. 📧 Outlook Not Receiving Emails

**Problem:** A user says they stopped receiving emails in Outlook.

**Steps to resolve:**
1. Check if the user has internet connectivity first
2. Look in the **Junk Email** and **Other** folders to rule out filtering
3. Check if Outlook is in **Work Offline** mode: Go to **Send/Receive** tab — if "Work Offline" is highlighted, click it to go back online
4. Check the mailbox storage quota in **Outlook** > File > Info > Mailbox Settings
5. Remove and re-add the email account: File > Account Settings > remove account > add it back
6. If using Microsoft 365, check the **Microsoft 365 Service Health** dashboard for outages
7. Escalate to the email admin if the issue persists

---

### 8. 🖥️ Blue Screen of Death (BSOD)

**Problem:** A user's computer crashes with a blue screen and restarts unexpectedly.

**Steps to resolve:**
1. Note the **error code** displayed on the BSOD (e.g., KERNEL_SECURITY_CHECK_FAILURE)
2. Boot into Windows and open **Event Viewer** > Windows Logs > System
3. Look for critical errors around the time of the crash
4. Open **Reliability Monitor** (search in Start menu) for a timeline of errors
5. Run `sfc /scannow` in an elevated Command Prompt to repair corrupted system files
6. Run `chkdsk /f /r` to check for disk errors
7. Check if any new drivers or software were installed recently — roll them back if so
8. Update all drivers, especially GPU and chipset
9. If BSODs continue, test RAM using **Windows Memory Diagnostic**
10. Escalate for hardware replacement if a hardware fault is confirmed

---

### 9. 🔌 Computer Won't Turn On

**Problem:** A user presses the power button but nothing happens.

**Steps to resolve:**
1. Check that the power cable is firmly connected to both the computer and the outlet
2. Try a different power outlet to rule out an outlet issue
3. For laptops, connect the charger and wait 5 minutes before powering on
4. Check if any indicator lights appear when pressing the power button
5. For desktops, check that the power supply switch on the back is set to **ON (I)**
6. Perform a hard reset: unplug the power cable, hold the power button for 30 seconds, then reconnect and try again
7. For laptops, remove the battery (if removable), hold power for 30 seconds, reinsert battery, and try again
8. If the machine still won't turn on, escalate for hardware inspection (possible PSU or motherboard failure)

---

### 10. 🗂️ User Cannot Access a Shared Drive

**Problem:** A user receives "Access Denied" when trying to open a shared network drive.

**Steps to resolve:**
1. Confirm the user is logged in with the correct domain account
2. Check that the shared drive is mapped: open **File Explorer** > This PC and look for mapped drives
3. If not mapped, map it manually:
   - Right-click **This PC** > **Map network drive**
   - Enter the network path (e.g., `\\server\SharedDrive`)
   - Check **Reconnect at sign-in**
4. Open **ADUC** and verify the user is a member of the correct security group that has access to the drive
5. If not in the group, add them: open the group > Members tab > Add the user
6. Ask the user to sign out and sign back in to apply the new group membership
7. Test access again
8. If still denied, check the share and NTFS permissions on the server with the system admin

---
